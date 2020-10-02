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

Custom instances will use the same paths but with your custom domain name.

A JSON file for easy configuration via Canvas is provided at
[./carnap-lti-canvas.json](./carnap-lti-canvas.json).

After this configuration is set up, it must be configured on the Carnap
instance administration page at `/master_admin`. For setup with the public
Carnap instance at Carnap.io, [contact Graham](mailto:gleachkr@ksu.edu) with
the following details from your LMS:

* Public JWKs URL
* Authorization Redirect URL
* Client ID

For more details on Canvas setup with LTI 1.3, see:

* [Technical documentation](https://canvas.instructure.com/doc/api/file.lti_dev_key_config.html).
  This is also a nice general overview of the protocol.
* [Configuring an LTI key](https://community.canvaslms.com/t5/Admin-Guide/How-do-I-configure-an-LTI-key-for-an-account/ta-p/140)

## LTI Setup (Carnap side)

If you are running a self-hosted instance of Carnap, you can configure LTI
Platforms (Learning Management Systems) on the admin page at
`https://carnap.example.com/master_admin`.

For example, for a cloud Canvas (production environment):
- JWK URL: `https://canvas.instructure.com/api/lti/security/jwks`
- Authorization redirect URL: `https://canvas.instructure.com/api/lti/authorize_redirect`
- Client ID: from your LTI developer key
- Deployment ID: not required for Carnap
