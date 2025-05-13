# Integrate Wazuh 4.9 to Google Chat

This repository contains scripts to integrate Wazuh alerts with Google Chat. It includes:
- `custom-gchat`: The main script for the integration.
- `test-gchat-connection.py`: A test script to verify the Google Chat connection.

## Prerequisites

1. **Python Modules**: Ensure the following modules are installed using the Python package from Wazuh:
   ```bash
   /var/ossec/framework/python/bin/pip3 install httplib2
   /var/ossec/framework/python/bin/pip3 install requests
   ```

2. **File Location and Permissions**:
   - Place the scripts in `/var/ossec/integrations/`.
   - Set the appropriate permissions:
     ```bash
     chmod 750 /var/ossec/integrations/custom-gchat
     chown root:wazuh /var/ossec/integrations/custom-gchat
     ```

3. **Integration Configuration**:
   Add the following block to `/var/ossec/etc/ossec.conf`:
   ```xml
   <!-- Google Chat -->
   <integration>
     <name>custom-gchat</name>
     <alert_format>json</alert_format>
   </integration>
   ```

## Obtaining the Webhook URL

To integrate with Google Chat, you need a webhook URL. Follow these steps to generate it:

1. Go to the Google Workspace Developer guide on creating webhooks: [Google Chat Webhooks Quickstart](https://developers.google.com/workspace/chat/quickstart/webhooks).
2. Follow the instructions to set up a webhook for your Google Chat space.
   - Create a new Google Chat space or use an existing one.
   - Go to the space settings and select "Integrations".
   - Add a new webhook, provide it a name, and copy the generated URL.
3. Replace the placeholder webhook URL in the scripts with your actual webhook URL.

## Testing the Integration

Use the `test-gchat-connection.py` script to verify the connection to Google Chat:
```bash
python3 test-gchat-connection.py
```

## Main Script Overview

`custom-gchat` reads Wazuh alerts and sends formatted messages to a Google Chat space using the specified webhook URL.

## License

This integration is licensed under the GNU General Public License v2.
