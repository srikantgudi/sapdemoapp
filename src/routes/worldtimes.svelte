<svelte:head>
    <title>World Times</title>
</svelte:head>
<script>
    let zones = {
        LA: {name: 'Los Angeles', zone: 'America/Los_Angeles', ztime: ''},
        NY: {name: 'New York', zone: 'America/New_York', ztime: ''},
        UK: {name: 'United Kingdom', zone: 'Europe/London', ztime: ''},
        FR: {name: 'France', zone: 'Europe/Paris', ztime: ''},
        UAE: {name: 'Dubai', zone: 'Asia/Dubai', ztime: ''},
        IN: {name: 'India', zone: 'Asia/Kolkata', ztime: ''},
        JP: {name: 'Japan', zone: 'Asia/Tokyo', ztime: ''},
        PERTH: {name: 'Perth', zone: 'Australia/Perth', ztime: ''},
        SYDNEY: {name: 'Sydney', zone: 'Australia/Sydney', ztime: ''},
        NZ: {name: 'New Zealand', zone: 'Pacific/Auckland', ztime: ''}
    }

    let hdeg = 0;
    let mdeg = 0;
    let sdeg = 0;
    let tz = zones['IN'];

    let hclr = 'navy';

    const zoneTime = z => new Date().toLocaleString('en-US',{timeZone: z})

    $: {
        setInterval(() => {
            zones['IN'].ztime = zoneTime(zones['IN'].zone)
            zones['UAE'].ztime = zoneTime(zones['UAE'].zone)
            zones['FR'].ztime = zoneTime(zones['FR'].zone)
            zones['UK'].ztime = zoneTime(zones['UK'].zone)
            zones['NY'].ztime = zoneTime(zones['NY'].zone)
            zones['LA'].ztime = zoneTime(zones['LA'].zone)
            zones['PERTH'].ztime = zoneTime(zones['PERTH'].zone)
            zones['SYDNEY'].ztime = zoneTime(zones['SYDNEY'].zone)
            zones['NZ'].ztime = zoneTime(zones['NZ'].zone)

            const d = new Date().toLocaleString('en-US',{timeZone: tz.zone})
            const dt = new Date(d);
            const hr = dt.getHours()
            const mi = dt.getMinutes()
            const se = dt.getSeconds()
            sdeg = (se * 6) - 90
            mdeg = (mi * 6 + se / 10) - 90
            hdeg = (hr * 30 + mi / 2) - 90

            if (hr < 6) {
                hclr = '#666';
            } else if (hr < 12) {
                hclr = 'blue';
            } else if (hr < 18) {
                hclr = 'teal';
            } else {
                hclr = 'navy';
            }
        }, 1000)
    }
</script>

<style>
    body {
        overflow: hidden;
    }
    .text {
        font-size: 0.8px;
        cursor: pointer;
    }
    .text.title {
        font-size: 1px;
        font-weight: 600;
    }
</style>

<main>
    <svg viewBox="0 0 90 40" style="box-shadow: 0 0 2px #999">
        <text x="50" y="3" text-anchor="middle" font-size="2.5">WORLD TIMES</text>
        <text x="50" y="5" text-anchor="middle" font-size="1">Click the zone name to view analog clock</text>

        <ellipse fill="lightcyan" stroke="blue" stroke-width="0.2" rx="36" ry="15" cx="50" cy="22" />

        <text x="25" y="20" text-anchor="middle" class="text title" on:click={() => tz=zones['LA']} fill={zones['LA'].zone===tz.zone ? 'blue' : '#999'}>{zones['LA'].name}</text>
        <text x="25" y="21" text-anchor="middle" class="text">{zones['LA'].ztime}</text>
        <text x="32" y="17" text-anchor="middle" class="text title" on:click={() => tz=zones['NY']} fill={zones['NY'].zone===tz.zone ? 'blue' : '#999'}>{zones['NY'].name}</text>
        <text x="32" y="18" text-anchor="middle" class="text">{zones['NY'].ztime}</text>
        <text x="39" y="13" text-anchor="middle" class="text title" on:click={() => tz=zones['UK']} fill={zones['UK'].zone===tz.zone ? 'blue' : '#999'}>{zones['UK'].name}</text>
        <text x="39" y="14" text-anchor="middle" class="text">{zones['UK'].ztime}</text>
        <text x="43" y="16" text-anchor="middle" class="text title" on:click={() => tz=zones['FR']} fill={zones['FR'].zone===tz.zone ? 'blue' : '#999'}>{zones['FR'].name}</text>
        <text x="43" y="17" text-anchor="middle" class="text">{zones['FR'].ztime}</text>
        <text x="48" y="18" class="text title" text-anchor="middle" on:click={() => tz=zones['UAE']} fill={zones['UAE'].zone===tz.zone ? 'blue' : '#999'}>{zones['UAE'].name}</text>
        <text x="48" y="19" text-anchor="middle" class="text">{zones['UAE'].ztime}</text>
        <text x="54" y="20" class="text title" text-anchor="middle" on:click={() => tz=zones['IN']} fill={zones['IN'].zone===tz.zone ? 'blue' : '#999'}>{zones['IN'].name}</text>
        <text x="54" y="21" text-anchor="middle" class="text">{zones['IN'].ztime}</text>
        <text x="60" y="25" class="text title" text-anchor="middle" on:click={() => tz=zones['PERTH']} fill={zones['PERTH'].zone===tz.zone ? 'blue' : '#999'}>{zones['PERTH'].name}</text>
        <text x="60" y="26" text-anchor="middle" class="text">{zones['PERTH'].ztime}</text>
        <text x="68" y="24" class="text title" text-anchor="middle" on:click={() => tz=zones['SYDNEY']} fill={zones['SYDNEY'].zone===tz.zone ? 'blue' : '#999'}>{zones['SYDNEY'].name}</text>
        <text x="68" y="25" text-anchor="middle" class="text">{zones['SYDNEY'].ztime}</text>
        <text x="73" y="22" class="text title" text-anchor="middle" on:click={() => tz=zones['NZ']} fill={zones['NZ'].zone===tz.zone ? 'blue' : '#999'}>{zones['NZ'].name}</text>
        <text x="73" y="23" text-anchor="middle" class="text">{zones['NZ'].ztime}</text>

        <circle fill="aliceblue" stroke-width="0.1" stroke="grey" r="8" cx="40" cy="28" />
        <polyline fill={hclr} points="40,28 41,28.3 45,28 41,27.7 40,28" transform={`rotate(${hdeg} 40 28)`} />
        <polyline fill={hclr} points="40,28 41,28.2 47,28 41,27.8 40,28" transform={`rotate(${mdeg} 40 28)`} />
        <polyline fill="olive" points="40,28 41,28.1 48,28 41,27.9 40,28" transform={`rotate(${sdeg} 40 28)`} />
        <text x="40" y="32" text-anchor="middle" class="text title" fill={hclr}>{tz.name}</text>
        <text x="40" y="33" text-anchor="middle" class="text" fill={hclr}>{tz.zone}</text>

        <animate xlink:href="#zn" attributeName="opacity" from="0.1" to="1" repeatCount="indefinite" dur="1" />
    </svg>
</main>