<style>
h4 {
    padding-top: 1em;
    padding-bottom: .3em;
    border-bottom: 1.5px solid #aaa;
}

h2 {
    margin-bottom: .5em;
}
</style>

# Carnap API

Carnap has an experimental API, which is not released yet (see the tracking
issues below).

## Tracking issues

* [Issue #226 "Perform instructor actions via an API"](https://github.com/Carnap/Carnap/issues/226)
* [Issue #231 "Documents API"](https://github.com/Carnap/Carnap/issues/231)
* [Issue #230 "Copy course"](https://github.com/Carnap/Carnap/issues/230)

## Instructor setup

You can add an API key on the instructor page on the "Manage Uploaded
Documents" page here:

![image showing the API key field at the bottom of the screen](images/apikey.png)

## Usage

### Test harness

I used the following setup to produce these examples:

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

Then `ipython -i apitest.py`, or `python -i apitest.py`

## Methods

### Document API

All of the methods in the documents API require that `:instructorIdent` is
the same as the user who owns the API key (i.e. they do not work on other
users' documents yet).

[Tracking issue](https://github.com/Carnap/Carnap/issues/231)

#### GET `/instructor/:instructorIdent/documents`

Retrieves a list of documents owned by the given instructor and their metadata.

Example:

```python
In: rq('GET', '/instructor/yourname@gmail.com/documents').json()
Out:
[{'creator': 1,
  'date': '2021-02-16T09:41:39.445672522Z',
  'scope': 'Public',
  'id': 1,
  'description': None,
  'filename': 'api.md'}]
```

#### POST `/instructor/:instructorIdent/documents`

Creates a new document with empty contents. Should be followed by a `PUT` at
`/instructor/:instructorIdent/documents/:documentId/data` in order to fill in
the document contents

Example:

```python
In: rq('POST','/instructor/gleachkr@gmail.com/documents', data='{"filename":"myfile.md","scope":"Private", "description":"My file"}').json()
Out: The ID of your new document
```

The response will also include a `Location` header pointed at the new resource.
`scope` indicates the sharing scope of the document, and can be one of
`Private`, `Public`, `LinkOnly` or `InstructorsOnly`. Both the scope and
description fields can be omitted, with scope defaulting to `Private`.

#### GET `/instructor/:instructorIdent/documents/:documentId`

Like GET `/instructor/:instructorIdent/documents` but for a single document.

Example:

```python
In: rq('GET', '/instructor/yourname@gmail.com/documents/1').json()
Out:
{'creator': 1,
 'date': '2021-02-16T09:41:39.445672522Z',
 'scope': 'Public',
 'description': None,
 'filename': 'api.md'}
```

#### PATCH `/instructor/:instructorIdent/documents/:documentId`

Updates the metadata for a single document

Example:

```python
In: rq('PATCH','/instructor/yourname@gmail.com/documents/1', data='{"scope":"Private"}').json()
Out:
{'creator': 1,
 'date': '2021-02-16T09:41:39.445672522Z',
 'scope': 'Private',
 'description': None,
 'filename': 'api.md'}
```

Currently `scope` and `description` fields can be updated. Passing in a null
value for `description` will cause the document description to be cleared
entirely.

#### GET `/instructor/:instructorIdent/documents/:documentId/data`

Gets the content of the given document by ID and returns it.

```python
In: rq('GET', '/instructor/jade@lfcode.ca/documents/1/data').text
Out: 'aaaaaa'
```

#### PUT `/instructor/:instructorIdent/documents/:documentId/data`

Overwrites the content of the given document by ID.

```python
In: rq('PUT', '/instructor/yourname@gmail.com/documents/1/data', data='aaaaaa')
Out: <Response [200]>
```
