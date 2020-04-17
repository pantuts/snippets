```
from mailjet_rest import Client

mailjet = Client(auth=(API_KEY, API_SECRET), version='v3.1')
DATA = {
    'Messages': [
        {
            'From': {
                'Email': EMAIL_FROM,
                'Name': NAME_FROM
            },
            'To': [
                {
                    'Email': EMAIL_TO,
                    'Name': NAME_TO
                }
            ],
            'Subject': '',
            'TextPart': '',
            'Attachments': []
        }
    ]
}


def mail_jet(subj: str, body: str, att=None):
    DATA['Messages'][0]['Subject'] = subj
    DATA['Messages'][0]['TextPart'] = body
    if att:
        DATA['Messages'][0]['Attachments'] = att
    try:
        mailjet.send.create(data=DATA)
        return True
    except Exception as e:
        return False
```