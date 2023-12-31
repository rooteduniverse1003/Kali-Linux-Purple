# <a name="Alerting"></a>Alerting

* [Alerting](#Alerting)
    - [Email Sender Accounts](#AlertingEmail)

Malcolm uses the Alerting plugins for [OpenSearch](https://github.com/opensearch-project/alerting) and [OpenSearch Dashboards](https://github.com/opensearch-project/alerting-dashboards-plugin). See [Alerting](https://opensearch.org/docs/latest/monitoring-plugins/alerting/index/) in the OpenSearch documentation for usage instructions.

A fresh installation of Malcolm configures an example [custom webhook destination](https://opensearch.org/docs/latest/monitoring-plugins/alerting/monitors/#create-destinations) named **Malcolm API Loopback Webhook** that directs the triggered alerts back into the [Malcolm API](api.md#API) to be reindexed as a session record with `event.dataset` set to `alerting`. The corresponding monitor **Malcolm API Loopback Monitor** is disabled by default, as you'll likely want to configure the trigger conditions to suit your needs. These examples are provided to illustrate how triggers and monitors can interact with a custom webhook to process alerts.

## <a name="AlertingEmail"></a>Email Sender Accounts

When using an email account to send alerts, you must [authenticate each sender account](https://opensearch.org/docs/latest/monitoring-plugins/alerting/monitors/#authenticate-sender-account) before you can send an email. The [`auth_setup`](authsetup.md#AuthSetup) script can be used to securely store the email account credentials:

```
./scripts/auth_setup 

Store administrator username/password for local Malcolm access? (Y/n): n

(Re)generate self-signed certificates for HTTPS access (Y/n): n

(Re)generate self-signed certificates for a remote log forwarder (Y/n): n

Store username/password for primary remote OpenSearch instance? (y/N): n

Store username/password for secondary remote OpenSearch instance? (y/N): n

Store username/password for email alert sender account? (y/N): y

Email account username: analyst@example.org
analyst@example.org password: 
analyst@example.org password (again): 
Email alert sender account variables stored: opensearch.alerting.destination.email.destination_alpha.password, opensearch.alerting.destination.email.destination_alpha.username

(Re)generate internal passwords for NetBox (Y/n): n
```

This action should only be performed while Malcolm is [stopped](running.md#StopAndRestart): otherwise the credentials will not be stored correctly.