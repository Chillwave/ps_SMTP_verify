# SMTP Connection Verification Tool

This tool is designed as a lightweight solution for verifying SMTP server connections specifically for the "Scan to Email" feature on printers. It uses PowerShell to send a test email, ensuring that the SMTP relay settings and credentials are correctly configured.

## Prerequisites

- Ensure you have PowerShell installed on your system.
- You need appropriate permissions to execute scripts on your machine.

## Configuration

1. **Set up SMTP Credentials and Server Details:**

   Open your PowerShell prompt and enter the following commands, replacing the placeholders with your actual SMTP server details and credentials:

   ```powershell
   $smtpServer = "<SMTP_SERVER_ADDRESS>"
   $smtpPort = <SMTP_PORT>  # typically 587 for TLS
   $username = "<YOUR_USERNAME>"
   $password = ConvertTo-SecureString "<YOUR_PASSWORD>" -AsPlainText -Force
   $credential = New-Object System.Management.Automation.PSCredential($username, $password)
   ```

   Replace the placeholders:
   - `<SMTP_SERVER_ADDRESS>` with your SMTP server URL, e.g., `us-smtp-outbound-1.mimecast.com`.
   - `<SMTP_PORT>` with the server port, e.g., `587`.
   - `<YOUR_USERNAME>` and `<YOUR_PASSWORD>` with your SMTP service credentials.

2. **Prepare the Email Content:**

   Set the sender, recipient, subject, and body of the test email:

   ```powershell
   $from = "<SENDER_EMAIL>"
   $to = "<RECIPIENT_EMAIL>"
   $subject = "Test Email - SMTP Relay Verification"
   $body = "This is a test email sent from SMTP using TLS to verify the provided credentials are functioning."
   ```

   Update `<SENDER_EMAIL>` and `<RECIPIENT_EMAIL>` with the respective email addresses.

## Running the Tool

After configuring your variables, execute the following command to send the test email:

```powershell
Send-MailMessage -SmtpServer $smtpServer -Port $smtpPort -UseSsl -Credential $credential -From $from -To $to -Subject $subject -Body $body
```

## Expected Outcome

- Check the inbox of the recipient (`<RECIPIENT_EMAIL>`) to confirm whether the test email was received.
- If correctly configured and the login credentials are working, the email should appear in the inbox without any errors.
- Ensure to verify the security aspects and the log entries, if applicable, to monitor the communication.

## Troubleshooting

If you do not receive the email:
- Verify that all credentials and server details are correct.
- Check your spam folder and the server’s security settings.
- Review the firewall settings that may block email relays.
- Consult the SMTP server logs for further diagnosis.

---

Make sure to replace placeholders with the actual data needed when using the script in your environment.
