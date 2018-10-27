# erlcaptcha - reCAPTCHA validation for Erlang/OTP applications

`erlcaptcha` is an OTP Application that is able to verify reCAPTCHA (v2 and v3) responses from Erlang applications.

## Using erlcaptcha

Add erlcaptcha to your list of dependencies within `rebar.config`:

```erl
%% rest of rebar.config
{deps, [
    %% other deps
    {erlcaptcha, "~>1.0"}
]}.
```

Use an [application configuration file](https://www.rebar3.org/docs/releases#section-application-configuration) like `sys.config` to configure your Google reCAPTCHA secret:

```erl
[
  {erlcaptcha, [{secret, <<"YOUR_SECRET_RECAPTCHA_API_KEY">>}]}
].
```

If this does not work for you, you can manually set the application environment somewhere else in your code (preferably before the erlcaptcha process is started):

```erl
application:set_env(erlcaptcha, secret, ?YOUR_SECRET_RECAPTCHA_API_KEY).
```

### API
- `verify/1`, `verify/2`: submits an HTTP POST request to the reCAPTCHA API passing in the response you received from the frontend, and optionally the client's IP as well.

### Response types
If errors occur, erlcaptcha will return `{errors, [error1, error2]}` as per the API documentation. For successful requests, erlcaptcha returns a proplist with all the documented response parameters: `success`, `challenge_ts`, `hostname`, `score` and `action`.

## Contributing
We welcome collaboration on this project and we gladly accept pull requests that implement new features or that otherwise improve our code.
