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
                hclr = 'darkgrey';
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
    .text {
        font-size: 10px;
        cursor: pointer;
    }
    .text.title {
        font-size: 12px;
        font-weight: 600;
    }
</style>

<main>
    <svg height="400" width="1000">
        <ellipse id="earth" rx="410" ry="200" cx="420" cy="200" stroke="lightblue" fill="lightcyan" />
        <ellipse id="earth" rx="380" ry="150" cx="420" cy="200" stroke="lightblue" fill="lightblue">
            <animate attributeName="rx" values="380;320;200;50;200;320;380" dur="5s" begin="0" repeatCount="indefinite" />
            <animate attributeName="ry" values="150;100;50;100;150" dur="3s" begin="0" repeatCount="indefinite" />
            <animate attributeName="fill" values="lightblue;lightcyan;whitesmoke;lightcyan;lightblue;" dur="3s" begin="0" repeatCount="indefinite" />
        </ellipse>

        <rect x="310" y="20" width="180" height="30" fill="lightcyan" stroke="grey" />
        <text x="400" y="40" font-size="20px" text-anchor="middle" fill="blue">World Times
            <animate attributeName="font-size" values="20;10;25" dur="5" begin="0" repeatCount="indefinite" />
        </text>
        <text x="400" y="66" font-size="12px" text-anchor="middle" fill="blue">
        Click on the zone name to view the clock
            <animate attributeName="fill" values="navy;olive;blue;olive;navy" dur="10" begin="0" repeatCount="indefinite" />
        </text>

        <!-- clock for the selected zone -->
        <circle r="90" cx="200" cy="250" fill="aliceblue" stroke="blue" stroke-width="2" />
        <polyline points="200,250 205,255 260,250 205,245 200,250" transform={`rotate(${hdeg} 200 250)`} fill={hclr} />
        <polyline points="200,250 205,254 280,250 205,246 200,250" transform={`rotate(${mdeg} 200 250)`} fill={hclr} />
        <polyline points="200,250 205,252 280,250 205,248 200,250" transform={`rotate(${sdeg} 200 250)`} fill="brown" />
        <text x="200" y="280" text-anchor="middle" font-size="14" font-weight="600" fill="blue">{tz.name}</text>

        <text x="100" y="160" text-anchor="middle" class="text title" on:click={() => tz=zones['LA']} fill={zones['LA'].zone===tz.zone ? 'blue' : '#999'}>{zones['LA'].name}</text>
        <text x="100" y="170" text-anchor="middle" class="text">{zones['LA'].ztime}</text>
        <text x="150" y="120" font-weight="600" text-anchor="middle" class="text title" on:click={() => tz=zones['NY']} fill={zones['NY'].zone===tz.zone ? 'blue' : '#999'}>{zones['NY'].name}</text>
        <text x="150" y="130" text-anchor="middle" font-size="12px" class="text">{zones['NY'].ztime}</text>
        <text x="250" y="80" text-anchor="middle" class="text title" on:click={() => tz=zones['UK']} fill={zones['UK'].zone===tz.zone ? 'blue' : '#999'}>{zones['UK'].name}</text>
        <text x="250" y="90" text-anchor="middle" class="text">{zones['UK'].ztime}</text>
        <text x="300" y="120" text-anchor="middle" class="text title" on:click={() => tz=zones['FR']} fill={zones['FR'].zone===tz.zone ? 'blue' : '#999'}>{zones['FR'].name}</text>
        <text x="300" y="130" text-anchor="middle" class="text">{zones['FR'].ztime}</text>
        <text x="350" y="180" class="text title" text-anchor="middle" on:click={() => tz=zones['UAE']} fill={zones['UAE'].zone===tz.zone ? 'blue' : '#999'}>{zones['UAE'].name}</text>
        <text x="350" y="190" text-anchor="middle" class="text">{zones['UAE'].ztime}</text>
        <text x="450" y="200" class="text title" text-anchor="middle" on:click={() => tz=zones['IN']} fill={zones['IN'].zone===tz.zone ? 'blue' : '#999'}>{zones['IN'].name}</text>
        <text x="450" y="210" text-anchor="middle" class="text">{zones['IN'].ztime}</text>
        <text x="550" y="240" class="text title" text-anchor="middle" on:click={() => tz=zones['PERTH']} fill={zones['PERTH'].zone===tz.zone ? 'blue' : '#999'}>{zones['PERTH'].name}</text>
        <text x="550" y="250" text-anchor="middle" class="text">{zones['PERTH'].ztime}</text>
        <text x="650" y="220" class="text title" text-anchor="middle" on:click={() => tz=zones['SYDNEY']} fill={zones['SYDNEY'].zone===tz.zone ? 'blue' : '#999'}>{zones['SYDNEY'].name}</text>
        <text x="650" y="230" text-anchor="middle" class="text">{zones['SYDNEY'].ztime}</text>
        <text x="750" y="210" class="text title" text-anchor="middle" on:click={() => tz=zones['NZ']} fill={zones['NZ'].zone===tz.zone ? 'blue' : '#999'}>{zones['NZ'].name}</text>
        <text x="750" y="220" text-anchor="middle" class="text">{zones['NZ'].ztime}</text>

        <animate xlink:href="#zn" attributeName="opacity" from="0.1" to="1" repeatCount="indefinite" dur="1" />
    </svg>
</main>