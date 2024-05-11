# Authentication to GitHub

## Token

- Connect runner to GitHub via configuration token
- Only valid for 1 hour and can only use for installing runners
- Alternatively create installation token via REST API on demand
    - `POST https://api.github.com/repos/{OWNER}/{REPO}/actions/runners/registration-token`
    - organizational level `https://api.github.com/orgs/{ORG}/actions/runners/registration-token`

## Example to Receive Token via Personal Access Token (PAT)

```
$ curl -L \
> -X POST \
> -H "Accept: application/vnd.github+json" \
> -H "Authorization: Bearer <YOUR-PAT>" \
> -H "X-GitHub-Api-Version: 2022-11-28" \
> https://api.github.com/repos/{OWNER}/{REPO}/actions/runners/registration-token
```

## Capture Token

```
$ TOKEN=$(<curl command> | jq .token --raw-output)
```

## Registration

- Token only valid for registration
- During registration process, a JWT (JSON Web Token for OAuth exchange) will be received from the
  server that only has permission to listen to queue
- When a workflow run starts, another pre-built token with a limited scope (defined by the workflow)
  will be created for the life of the build
- That token cannot be accessed via ad hoc scripts or untrusted code – only by build agent and tasks
- The RSA private key for the OAuth token exchange between agent and server will be stored
  in `.credentials_rsaparams` and server holds the public key
- Every 50 minutes, server will send a new token to agent that's encrypted by public key
- OAuth configuration is stored in the `.credentials`

```
{
  "scheme": "OAuth",
  "data": {
    "clientId": "{CLIENT_ID}",
    "authorizationUrl": "https://pipelinesghubeus4.actions.
    githubusercontent.com/{TOKEN}/_apis/oauth2/token",
    "requireFipsCryptography": "True"
  }
  
}
```

## Running Application as a Service

- Windows
    - configuration script asks to execute runner as a service to start alongside environment
- Linux
    - sudo ./svc.sh install
    - sudo ./svc.sh start

## Network Communication

- Communicates via an outgoing HTTPS connection on port 443
    - using long polling with 50-second timeout
- Means that app asks GitHub if any work is queued for labels of runner
    - then waits for 50 seconds for response before connection is closed
- Immediately after closing connection, new connection is started
- No need for any inbound connection from GitHub or to open any firewall ports
- Only secure outbound connections using SSL over port 443

## Cleanup

- Does not cleanup resources after a workflow run
    - unlike self-hosted runners that provide an ephemeral fresh environment for each workflow run
- Configure pre- and post-job script
- Save script to location which runner has access
- Configure an environment variable
    - ACTIONS_RUNNER_HOOK_JOB_STARTED
    - ACTIONS_RUNNER_HOOK_JOB_COMPLETED
- Alternatively, store key-value pairs in a `.env` file inside runner app directory
