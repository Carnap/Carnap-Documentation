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
[Configuring an LTI key](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-LTI-key-for-an-account/ta-p/140).
Canvas also allows configurations to be imported rather than set manually, via
the "Paste JSON" option described in the documentation linked above. A JSON
file for easy configuration of a canvas instance, using this method is provided
at [./carnap-lti-canvas.json](./carnap-lti-canvas.json).

For more details on Canvas setup with LTI 1.3, see:

* [Technical documentation](https://canvas.instructure.com/doc/api/file.lti_dev_key_config.html).
  This is also a nice general overview of the protocol.
* [Configuring an LTI key](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-LTI-key-for-an-account/ta-p/140)

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
