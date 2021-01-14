# LTI 1.3

Carnap supports [LTI 1.3](http://www.imsglobal.org/spec/lti/v1p3/) for login,
allowing it to be placed directly in a Canvas course. No previous versions
superseded by LTI 1.3 including LTI 1.0, 1.1, or 2.0 are supported.

Various major LMS implementations including Moodle and Canvas support LTI 1.3
natively.

## LTI setup in a Learning Management System

Carnap.io's configuration parameters are:

* `oidc_initiation_url`: https://carnap.io/auth/page/lti13/initiate
* `target_link_uri`: https://carnap.io
* Public JWK URL: https://carnap.io/auth/page/lti13/jwks
* Redirect URLs: https://carnap.io/auth/page/lti13/authenticate

If you are running your own instance of the Carnap server, you will use the
same paths but with your custom domain name replacing "carnap.io".

### Common LMS: Canvas

Instructions for configuring an LTI key for canvas can be found here:
[Configuring an LTI
key](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-LTI-key-for-an-account/ta-p/140).
This will require someone with administrator access to your Canvas instance, so
you may need to speak to someone in your IT department to get this set up.
Canvas allows configurations to be imported rather than set manually, via
the "Paste JSON" option described in the documentation linked above. A JSON
file for easy configuration of a canvas instance using this method is
reproduced below. The Canvas administrator will also need to *manually* set the
privacy level associated with the LTI key to *public*, so that Canvas will
share students' names with Carnap.

Once the LTI key is configured in your canvas instance, you'll need to ask your
canvas administrator for the client ID number associated with the key, and
follow the instructions here: [Adding Carnap To Your
Course](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-external-app-for-an-account-using-a-client/ta-p/202).

For more details on Canvas setup with LTI 1.3, see:

* [Technical documentation](https://canvas.instructure.com/doc/api/file.lti_dev_key_config.html).
  This is also a nice general overview of the protocol.
* [Configuring an LTI key](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-LTI-key-for-an-account/ta-p/140)
* [Adding Carnap To Your
Course](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-external-app-for-an-account-using-a-client/ta-p/202)

####JSON Configuration with Canvas.

```json
{
   "title": "Carnap",
   "description": "Carnap Logic Framework",
   "privacy_level": "public",
   "oidc_initiation_url": "https://carnap.io/auth/page/lti13/initiate",
   "target_link_uri": "https://carnap.io/",
   "public_jwk_url": "https://carnap.io/auth/page/lti13/jwks",
   "scopes": [
      "https://purl.imsglobal.org/spec/lti-ags/scope/lineitem",
      "https://purl.imsglobal.org/spec/lti-ags/scope/result.readonly",
      "https://purl.imsglobal.org/spec/lti-ags/scope/score",
      "https://purl.imsglobal.org/spec/lti-nrps/scope/contextmembership.readonly"
   ],
   "extensions": [
      {
         "domain": "carnap.io",
         "tool_id": "Carnap.io",
         "platform": "canvas.instructure.com",
         "settings": {
            "text": "Carnap",
            "selection_height": 800,
            "selection_width": 800,
            "placements": [
               {
                  "text": "Carnap",
                  "enabled": true,
                  "placement": "course_navigation",
                  "message_type": "LtiResourceLinkRequest",
                  "target_link_uri": "https://carnap.io/",
                  "windowTarget": "_blank"
               }
            ]
         }
      }
   ]
}
```

Note: It is possible to use Carnap in an `iframe` (so it appears in the Canvas
page without opening a new tab), but there are caveats, especially around
support for Safari and other WebKit browsers, since they are very aggressive
about third-party cookie blocking. If you want to try this, remove the
`"windowTarget": "_blank"` in the JSON.

## LTI Setup (Carnap side)

After your LTI provider is configured to talk to Carnap, it needs to be
registered on the Carnap server. For setup with the public Carnap instance at
Carnap.io, [contact Graham](mailto:gleachkr@ksu.edu) with the following details
from your LMS:

* Public JWKs URL
* Authorization Redirect URL
* Client ID

For example, for a cloud Canvas (production environment), these would be:

* JWK URL: `https://canvas.instructure.com/api/lti/security/jwks`
* Authorization redirect URL: `https://canvas.instructure.com/api/lti/authorize_redirect`
* Client ID: from your LTI developer key
* Deployment ID: not required for Carnap

If you are running a self-hosted instance of Carnap, you can configure LTI
Platforms (Learning Management Systems) on the admin page at
`https://carnap.example.com/master_admin`.

## Automatic registration

Automatic registration links a class on the Carnap server to a class in an LMS,
and automatically registers students in the Carnap class when they log in to
Carnap from the associated course in the LMS LMS.

### Setup

Set up LTI in your learning management system. Then, initiate a launch by
attempting to log in to Carnap from the LMS course that you want to connect to
Carnap. A message will appear on the carnap user registration page giving you
an autoregistration ID. Copy this ID down, and go to your instructor page on
Carnap. Select the course that you wish to associate with your LMS course, and
edit the course information. In the course information, there will be a field
where you can paste the autoregistration ID.

Once that ID has been configured, all future launches from your LMS course will
be registered in the associated Carnap course automatically.

### Notes

* Automatic registrations are allowed even if your course is closed (even if
you've unchecked the "course open" box on your instructor page). So, you can
set registration to be LTI only simply by setting your course to be closed.

* Students will have their user information automatically synchronized with the 
LMS on every launch, so if they want to change their name or other details,
that should be accomplished in the LMS or other upstream systems.

## Developer use

Setting up a Canvas instance or other LMS is quite burdensome for doing LTI
testing. Therefore, the UBC Carnap team has kindly set up a LTI Reference
Implementation platform here:

https://lti-ri.imsglobal.org/platforms/1255/

Configure it in Carnap at `/master_admin` with the following:

| iss	| client_id	| OIDC Auth Endpoint	| JWK URL |
| ---	| ---------	| ------------------	| ------- |
| aaaaa	| abcde	    | https://lti-ri.imsglobal.org/platforms/1255/authorizations/new	| https://lti-ri.imsglobal.org/platforms/1255/platform_keys/1248.json |

To perform launches, use the "Resource Links" page.
