<style> 

h4, h5 { 
    padding-top: 1em; 
    padding-bottom: .3em; 
    border-bottom: 1.5px solid #aaa; 
}

h2 {
    margin-bottom: .5em;
}

pre.sourceCode {
    background-color: #f8f8f8;
}

article img {
    max-width: 100%;
}
</style>

# Carnap API

Carnap has an experimental API, which is currently under development (see the
tracking issues below).

## Tracking issues

* [Issue #226 "Perform instructor actions via an API"](https://github.com/Carnap/Carnap/issues/226)
* [Issue #231 "Documents API"](https://github.com/Carnap/Carnap/issues/231)
* [Issue #230 "Copy course"](https://github.com/Carnap/Carnap/issues/230)

## Instructor setup

To use the API, you need an API key. Your API key should be kept a secret,
since it allows anyone who has it to access and modify your courses.

You can create an API key for yourself on the instructor page, beneath the
"Manage Uploaded Documents" tab, here:

![image showing the API key field at the bottom of the screen](images/apikey.png)

## Usage

### Example Scripts

Here are some examples to help you start using the API with different
programming languages. We assume that you're testing, so the URL begins with
`http://localhost:3000`. This should instead be `https://YOURSERVERRDOMAIN`
when you're using this with a non-local server

#### Python

Create the file `apitest.py`:

```python
import requests

apikey = 'REDACTED'

base = 'http://localhost:3000/api/v1'

def rq(meth, p, *args, key=apikey, **kwargs):
    h = {
        'X-API-KEY': key,
    }
    return requests.request(meth, base + p, *args, **kwargs, headers=h)
```

To issue the commands displayed below interactively `ipython -i apitest.py`, or
`python -i apitest.py`.

#### Bash

Just use `curl` as indicated below.

## Available API Methods

### Document API

All of the methods in the documents API require that `:instructorIdent` is
the same as the user who owns the API key (i.e. they do not work on other
users' documents yet).

[Tracking issue](https://github.com/Carnap/Carnap/issues/231)

##### GET `/instructors/:instructorIdent/documents`

<details> <summary> Retrieves a list of documents owned by the given instructor
and their metadata. </summary>

Here are some example commands:

*Python*

```python
rq('GET', '/instructors/yourname@gmail.com/documents').json()
```

*Bash*

```bash
curl -H "X-API-KEY:YOURAPIKEYHERE" localhost:3000/api/v1/instructors/yourname@youremail.com/documents
```

**Result**

And here's what your result will look like:

```python
[{'creator': 1,
  'date': '2021-02-16T09:41:39.445672522Z',
  'scope': 'Public',
  'id': 1,
  'description': None,
  'filename': 'api.md'}]
``` 

</details>

##### POST `/instructors/:instructorIdent/documents`

<details> <summary> Creates a new document with empty contents. </summary>

Should be followed by a `PUT` at
`/instructors/:instructorIdent/documents/:documentId/data` in order to fill in
the document contents.

*Python*

```python
rq('POST', '/instructors/yourname@gmail.com/documents',
    json={
        "filename": "myfile.md",
        "scope": "Private",
        "description": "My file",
    }
).json()
```

*Bash*

```bash
curl -H "X-API-KEY:YOURAPIKEY" \
     -H "Content-Type: application/json" \
     -d '{"filename":"myfile.md","scope":"Private", "description":"My file"}' \
     localhost:3000/api/v1/instructors/yourname@gmail.com/documents
```

**Result**

The ID of the new document:

```json
3
```

or an error is returned as an encoded JSON string.

The response will also include a `Location` header pointed at the new resource.
`scope` indicates the sharing scope of the document, and can be one of
`Private`, `Public`, `LinkOnly` or `InstructorsOnly`. Both the scope and
description fields can be omitted, with scope defaulting to `Private`.

</details>

##### GET `/instructors/:instructorIdent/documents/:documentId`

<details><summary> Like GET `/instructors/:instructorIdent/documents` but for a
single document. </summary>

*Python*

```python
rq('GET', '/instructors/yourname@gmail.com/documents/1').json()
```

*Bash*

```bash 
curl -H "X-API-KEY:YOURAPIKEYHERE" localhost:3000/api/v1/instructors/yourname@youremail.com/documents/1
```

**Result**

```python
{'creator': 1,
 'date': '2021-02-16T09:41:39.445672522Z',
 'scope': 'Public',
 'description': None,
 'filename': 'api.md'}
```

</details>

##### PATCH `/instructors/:instructorIdent/documents/:documentId`

<details><summary>Updates the metadata for a single document.</summary>

*Python*

```python
rq('PATCH', '/instructors/yourname@gmail.com/documents/1',
    json={"scope": "Private"}).json()
```

*Bash*

```bash 
curl -H "X-API-KEY:YOURAPIKEY" -X "PATCH" -d '{"scope":"Public"}' \
     localhost:3000/api/v1/instructors/yourname@youremail.com/documents/1
```

**Result**
```python
{'creator': 1,
 'date': '2021-02-16T09:41:39.445672522Z',
 'scope': 'Private',
 'description': None,
 'filename': 'api.md'}
```

Currently `scope` and `description` fields can be updated. Passing in a null
value for `description` will cause the document description to be cleared
entirely.

</details>

##### GET `/instructors/:instructorIdent/documents/:documentId/data`

<details><summary>Gets the content of the given document by ID and returns
it.</summary>

*Python*

```python
rq('GET', 'instructors/yourname@youremail.com/documents/1/data').text
```

*Bash*

```bash 
curl -H "X-API-KEY:YOURAPIKEYHERE" \
     localhost:3000/api/v1/instructors/yourname@youremail.com/documents/1/data
```

**Result**

The contents of your document, as text

</details>

##### PUT `/instructors/:instructorIdent/documents/:documentId/data`

<details><summary> Overwrites the content of the given document by ID.</summary> 

These examples use "aaaaaa" as a thing you might insert as the document
contents.

*Python*

```python
rq('PUT', '/instructors/yourname@gmail.com/documents/1/data', data='aaaaaa')
```

*Bash*

```sh
echo aaaaaa | curl -H "X-API-KEY:YOURAPIKEYHERE"  -T "-" \
    localhost:3000/api/v1/instructors/gleachkr@gmail.com/documents/1940/data
```

**Result**

```python
<Response [200]>
```

</details>

### Course API

Note: `:courseTitle` in the below needs to be properly URL-encoded for `curl`,
which means in particular that each space needs to be replaced with `%20`. The
python requests module does URL-encoding automatically, so spaces can be used
verbatim. The examples below are for a course with the title "test course".

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students`

<details><summary>Retrieves a list of student data for a given course,
including unique `:studentId` identifiers for each student.</summary>

```python
rq('GET', '/instructors/gleachkr@gmail.com/course/test course/students').json()
```

```sh
curl -H "X-API-KEY:YOURAPIKEYHERE" \
    'localhost:3000/api/v1/instructors/gleachkr@gmail.com/course/test%20course/students'
```

**Result**

```
[
  {
    "email": "groundworker@gmail.com",
    "lastName": "Kant",
    "universityId": null,
    "userId": 1231,
    "firstName": "Immanuel",
    "isAdmin": false,
    "id": 1313,
    "enrolledIn": 141,
    "instructorId": null,
    "isLti": false
  },
  {
    "email": "thinker@gmail.com",
    "lastName": "Descartes",
    "universityId": null,
    "userId": 1232,
    "firstName": "Rene",
    "isAdmin": false,
    "id": 1314,
    "enrolledIn": 141,
    "instructorId": null,
    "isLti": false
  },
]
```

The `:studentId` for a student is the number in the `id` field, *not* the
number in the `userId` field.

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId`

<details><summary>Retrieves student data for the student with id
`:studentId`</summary>

```python
rq('GET', '/instructors/gleachkr@gmail.com/course/test course/students/1231').json()
```

```sh
curl -H "X-API-KEY:YOURAPIKEYHERE" \
    'localhost:3000/api/v1/instructors/gleachkr@gmail.com/course/test%20course/students/1231'
```

**Result**

```
{
    "email": "groundworker@gmail.com",
    "lastName": "Kant",
    "universityId": null,
    "userId": 1231,
    "firstName": "Immanuel",
    "isAdmin": false,
    "id": 1313,
    "enrolledIn": 141,
    "instructorId": null,
    "isLti": false
}
```

The `:studentId` for a student is the number in `id` field, *not* the number in
the `studentId` field.

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId/submissions`

<details><summary>Retrieves a list of all submission data for the student with
id `:studentId` </summary>

```python
rq('GET', '/instructors/gleachkr@gmail.com/course/test course/students/1231/submissions').json()
```

```sh
curl -H "X-API-KEY:YOURAPIKEYHERE" \
    'localhost:3000/api/v1/instructors/gleachkr@gmail.com/course/test%20course/students/1231/submissions'
```

**Result**

```
[
  {
    'problemSubmissionAssignmentId': 3001, 
    'problemSubmissionCorrect': False, 
    'problemSubmissionData': {..depends on problem type..}, 
    'problemSubmissionSource': {'tag': 'Assignment', 'contents': 'AssignmentMetadataKey {unAssignmentMetadataKey = SqlBackendKey {unSqlBackendKey = 3001}}'}, 'problemSubmissionCredit': 1, 
    'problemSubmissionIdent': 'Exercise-24', 
    'problemSubmissionUserId': 10385, 
    'problemSubmissionLateCredit': None, 
    'problemSubmissionType': 'Qualitative', 
    'problemSubmissionTime': '2021-04-26T19:14:06.563900857Z', 
    'problemSubmissionExtra': None
  }
]
```

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId/extensions`

<details><summary>Retrieves a list of all assignment extensions granted to the
student with id `:studentId`</summary>

**RESULT**

``` 
[
  {
    "onAssignment": 1238,
    "until": "2022-06-02T04:59:59Z",
    "forUser": 12313,
    "id": 499
  }
]
```


</details>

##### POST `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId/extensions`

<details><summary>Grants an extension to the student with id
`:studentId`</summary>

```python
rq('POST', '/instructors/yourname@gmail.com/courses/test course/students/12313/extensions',
    json={
        "onAssignment": 2756,
        "until": "2022-06-02",
        "forUser": 12313,
    }
).json()
```

*Bash*

```bash
curl -H "X-API-KEY:YOURAPIKEY" \
     -H "Content-Type: application/json" \
     -d '{ "onAssignment": 2756, "until": "2022-06-02", "forUser": 12313 }' \
     localhost:3000/api/v1//instructors/yourname@gmail.com/courses/test%20course/students/12313/extensions
```

Dates can be given in the format "2021-06-30T21:40:00Z", for UTC time, or in
the format "2022-01-01 10:10" or simply "2022-01-01", in which case the date
will assume the time zone associated with the course.

The template for the POST JSON is:

```
{
  "onAsssignment": ...,
  "until": ...,
  "forUser": ...,
}
```

where the user field must the *userId* of the student, the contents of the
`userId` field of the data returned by GET
`https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId`,
*not* the contents of the `id` field returned by that GET request.

**Result**

The ID of the new document:

```json
3
```

or an error is returned as an encoded JSON string.

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId/accomodations`

<details><summary>Retrieves a list of accommodations active for the student
with id `:studentId`</summary>

So if the student's time allowed on exams is `(3 × STANDARD TIME) + 0 minutes`,
and they have their due-dates extended by one hour, then the result will be:

```
{
  "timeFactor": 3,
  "timeExtraMinutes": 0,
  "forUser": 1314,
  "id": 62,
  "dateExtraHours": 1,
  "forCourse": 121
}
```

</details>

##### PATCH `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId/accomodations`

<details><summary>Modifies the accommodations active for the student with id
`:studentId`</summary>

For example: 

```python
rq('PATCH', '/instructors/yourname@gmail.com/courses/test course/students/11231/accomodations',
    json={"timeFactor": "2"}).json()
```

*Bash*

```bash 
curl -H "X-API-KEY:YOURAPIKEY" -X "PATCH" \
     -H "Content-Type: application/json" \
     -d '{"timeFactor":"2"}' \
     /instructors/yourname@gmail.com/courses/test%20course/students/11231/accomodations
```

The template for the PATCH JSON (with all fields optional) is:

```
{
  "timeFactor": ...,
  "timeExtraMinutes": ...,
  "dateExtraHours": ...,
}
```

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/students/:studentId/assignmentTokens`

<details><summary>Retrieves a list of all access-restricted assignments that
have been accessed by the student with id `:studentId`, along with access time
for each.</summary>

**RESULT**

``` 
[
  {
    "createdAt": "2021-06-10T19:10:42.757612899Z",
    "user": 1,
    "id": 17927,
    "assignment": 3188
  }
]
```

</details>

##### DELETE `https://carnap.io/api/v1/instructor/:instructorIdent/courses/:courseTitle/students/:studentId/assignmentTokens/:tokenId`

<details><summary>Deletes the record of a student having accessed an
access-restricted assignment, allowing them to e.g. retake an exam for which a
certain amount of time was allotted.</summary>

**RESULT**

``` 
"deleted token" 
```

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/assignments`

<details><summary>Retrieves a list of assignments for a given course.</summary>

**RESULTS**

```
[
  {
    "gradeRelease": "2021-05-20T19:30:00Z",
    "totalProblems": null,
    "visibleFrom": "2021-05-19T17:58:00Z",
    "availability": null,
    "date": "2021-05-18T21:41:35.12705102Z",
    "document": 4293,
    "pointValue": null,
    "course": 258,
    "id": 3276,
    "duedate": "2021-05-19T19:30:00Z",
    "title": "The Hardest Logic Puzzle Ever",
    "visibleTill": "2021-06-30T21:40:00Z",
    "assigner": null,
    "description": null
  }
]
```

Times are reported in UTC

</details>

##### POST `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/assignments`

<details><summary>Creates a new assignment.</summary>

```python
rq('POST', '/instructors/yourname@gmail.com/courses/test course/assignments',
    json={
        "document": 2756,
        "title": "A new assignment",
        "due-date": "2022-01-01 10:10",
    }
).json()
```

*Bash*

```bash
curl -H "X-API-KEY:YOURAPIKEY" \
     -H "Content-Type: application/json" \
     -d '{"document": 2756, "title": "A new assignment", "due-date": "2022-01-01 10:10"}' \
     localhost:3000/api/v1/instructors/yourname@gmail.com/courses/test%20course/assignments
```

The full template for the POST json is 

```
  {
    "gradeRelease": ...,
    "totalProblems": ...,
    "visibleFrom": ...,
    "availability": ...,
    "document": ...,
    "pointValue": ...,
    "duedate": ...,
    "title": ...,
    "visibleTill": ...,
    "description": ...
  }
```

The only mandatory fields are `document` and `title`. Dates can be given in the
format "2021-06-30T21:40:00Z", for UTC time, or in the format "2022-01-01
10:10" or simply "2022-01-01", in which case the date will assume the time zone
associated with the course.

**RESULT**

The ID of the new assignment:

```json
3
```

or an error is returned as an encoded JSON string.

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/assignments/:assignmentId`

<details><summary>Retrieves the details of the assignment with id
`:assignmentId` .</summary> 

**RESULT**

```
{
  "gradeRelease": "2021-05-20T19:30:00Z",
  "totalProblems": null,
  "visibleFrom": "2021-05-19T17:58:00Z",
  "availability": null,
  "date": "2021-05-18T21:41:35.12705102Z",
  "document": 4293,
  "pointValue": null,
  "course": 258,
  "id": 3276,
  "duedate": "2021-05-19T19:30:00Z",
  "title": "The Hardest Logic Puzzle Ever",
  "visibleTill": "2021-06-30T21:40:00Z",
  "assigner": null,
  "description": null
}
```

</details>

##### PATCH `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/assignments/:assignmentId`

<details><summary>Modifies the details of the assignment with id `:assignmentId` .</summary>

For example: 

```python
rq('PATCH', '/instructors/yourname@gmail.com/courses/test course/assignments/1313',
    json={"gradeRelease": "2022-02-02"}).json()
```

*Bash*

```bash 
curl -H "X-API-KEY:YOURAPIKEY" -X "PATCH" \
     -H "Content-Type: application/json" \
     -d '{"gradeRelease": "2022-02-02"}' \
     /instructors/yourname@gmail.com/courses/test%20course/assignments/1313
```

The template for the PATCH JSON (with all fields optional) is:

```
{
  "gradeRelease": ...,
  "totalProblems": ...,
  "visibleFrom": ...,
  "availability": ...,
  "pointValue": ...,
  "duedate": ...,
  "title": ...,
  "visibleTill": ...,
  "description": ..., 
}
```

To delete the contents of any field, except for `title`, you can send an
explicit `null` value in the patch for that field.

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/assignments/:assignmentId/submissions`

<details><summary>Retrieves a list of all submitted problems for the assignment with id `:assignmentId` .</summary>

**RESULT**

```
[
  {
    'problemSubmissionAssignmentId': 3001, 
    'problemSubmissionCorrect': False, 
    'problemSubmissionData': {..depends on problem type..}, 
    'problemSubmissionSource': {'tag': 'Assignment', 'contents': 'AssignmentMetadataKey {unAssignmentMetadataKey = SqlBackendKey {unSqlBackendKey = 3001}}'}, 'problemSubmissionCredit': 1, 
    'problemSubmissionIdent': 'Exercise-24', 
    'problemSubmissionUserId': 10385, 
    'problemSubmissionLateCredit': None, 
    'problemSubmissionType': 'Qualitative', 
    'problemSubmissionTime': '2021-04-26T19:14:06.563900857Z', 
    'problemSubmissionExtra': None
  }
]
```

</details>

##### GET `https://carnap.io/api/v1/instructors/:instructorIdent/courses/:courseTitle/assignments/:assignmentId/submissions/:studentId`

<details><summary>Retrieves a list of all submitted problems from the student
with id `:studentId`, for the assignment with id `:assignmentId` .</summary>

**RESULT**

```
[
  {
    'problemSubmissionAssignmentId': 3001, 
    'problemSubmissionCorrect': False, 
    'problemSubmissionData': {..depends on problem type..}, 
    'problemSubmissionSource': {'tag': 'Assignment', 'contents': 'AssignmentMetadataKey {unAssignmentMetadataKey = SqlBackendKey {unSqlBackendKey = 3001}}'}, 'problemSubmissionCredit': 1, 
    'problemSubmissionIdent': 'Exercise-24', 
    'problemSubmissionUserId': 10385, 
    'problemSubmissionLateCredit': None, 
    'problemSubmissionType': 'Qualitative', 
    'problemSubmissionTime': '2021-04-26T19:14:06.563900857Z', 
    'problemSubmissionExtra': None
  }
]
```

</details>
