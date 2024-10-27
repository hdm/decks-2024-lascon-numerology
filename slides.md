---
theme: ./
title: Hacker Numerology
class: text-center
drawings:
  persist: true
transition: none
download: true
mdc: true
overviewSnapshots: true
aspectRatio: 16/9
background: /cover-bg.jpg
fonts:
  sans: Plus Jakarta Sans
  serif: Plus Jakarta
  mono: Fira Code
titleTemplate: "%s"
info: false
author: HD Moore
keywords: numerology,research,mac,runzero
wakeLock: true
favicon: /favicon.png
routerMode: hash
---

# Hacker Numerology

<div class="text-2xl">
  HD Moore
</div>


<div grid="~ cols-3 gap-25" class="abs-b text-sm color-gray m-5 font-weight-bold" m="t-3">
  <div>LASCON</div>
  <div>OCTOBER 25, 2024</div>
  <div>AUSTIN, TX</div>
</div>

 <div class="abs-tl m-5 flex gap-2 opacity-85">
  <img src="/lascon.png" width="200px">
</div>

<div class="abs-tr m-5 flex gap-2 opacity-85">
 <img src="/runzero.svg" width="200px">
</div>

<!--
This talk explores the numbers that define our lives and how to use limited observations of identifiers to reason about the security properties of systems.
-->

---
layout: image-right
image: /bellingthecat.jpg
---

# <img src="/bellingcat.svg" class="w-75">

<div class="mt-10 mb-10 text-2xl">
This presentation is dedicated to Bellingcat, who hold authorities accountable for human rights abuses, world-world, at extreme personal risk, through open source research.
</div>

https://Bellingcat.com/

<!--
-->



---
layout: image-left
image: /take-a-number.png
---


# Now serving...

<ul>
<li class="v-click">You receive ticket number <span class="neonGreen">74</span></li>
<v-click><li>What does this tell you?</li></v-click>
<v-click><li>Now serving number <span class="neonYellow">82</span></li></v-click>
<v-click><li>Now serving number <span class="color-red">85</span></li></v-click>
<v-click><li>Now serving number <span class="neonGreen">67</span></li>
<div class="abs-br font-bold color-white mb-2 mr-14 text-sm">https://en.wikipedia.org/wiki/German_tank_problem</div>
</v-click>
</ul>

<!--
You need to visit the DMV and are greeted by the dreaded "take a number" sign.
You grab a number and sit down, your number is 74.
Does 74 mean anything yet?
Wait for the next announcement
Now serving 82? Uh oh, is this a 1-100 system?
Now serving 84? Not great, this could be a long trip.
Now serving 67? Phew, ok, we have a chance of getting out of here soon.

So far, we've heard numbers as sets of two digits, we've heard higher numbers than we have, but also lower numbers.
They seem to be going through one number per minute, but the ordering isnt obvious.
Is the next number going to be 68, 87, or something else?

We're going to focus on this problem set. 
How can we understand a system through limited samples?

-->

---

# Every thing has an identifier

<div grid="~ cols-2 gap-10" m="t-2">

<div>

* Credit cards
* Documents
* Babies
* Patents
* Cables
* Passports

</div>

<div>

* Phones
* Cars
* Pets
* Receipts
* Web requests
* PINs

</div>
</div>

<v-click>
<p class="pt-20 text-2xl font-mono"><span class="text-5xl text-gray">&ldquo;</span> Now serving customer <UnixTS/>...</p>
</v-click>

<!--
we love to assign identifiers. We are obsessed with giving every thing, process, and moment a unique ID.

Every nanosecond we sit here has a unique ID that is being stored somewhere.
-->

---


# Most identifiers are short

* Entering long numbers is a hassle and error-prone
* The result is that identifiers are _dense_
* Information is encoded everywhere

<div class="mt-10"/>
<v-click>

## Ex: Social security numbers

<div class="mt-2"/>

* The first set of three digits is called the Area Number
* The second set of two digits is called the Group Number
* The final set of four digits is the Serial Number

<div class="abs-bl font-bold color-white ml-67 mb-2 text-lg">https://www.ssa.gov/employer/ssnvhighgroup.htm</div>

</v-click>



---
title: PINs
---

# PINs

* User-chosen IDs are the worst
* Short and predictable


<div grid="~ cols-3" m="t-3">

<div class="m-2">

>Statistically, one third of all codes can be guessed by trying just 61 distinct combinations!

</div>
<div/>
</div>


<img src="/pins-1.png" class="abs-tr border-3 m-3" width="50%">

<v-click>
<div class="mx-auto mt-3">
<img src="/pins-2.png" class="float-left mr-5" width="20%">
<img src="/pins-3.png" class="" width="20%">
</div>
</v-click>

<div class="abs-bl font-bold color-white ml-67 mb-2 text-lg">http://www.datagenetics.com/blog/september32012/</div>

---

# Every identifier is also a number

<ul class="mb-10">
<li class="v-click">Dell service tags are in the form of <span class="neonGreen">HGJSQY1</span></li>
<v-click><li>This is a Base36 (0-9A-Za-z) encoded decimal number</li></v-click>
<v-click><li>This converts to Express ID <span class="neonYellow">380-060-125-21</span></li></v-click>
<v-click><li>Flatten this to decimal <span class="neonYellow">38,006,012,521</span></li></v-click>
</ul>

<v-click><div>Identifiers often include categories, sequence numbers, and checksums</div></v-click>
<v-click><div class="mt-4">Vehicle Identification Numbers are a great example</div></v-click>

<!--
In some shape or form, every ID is a numeric value.
-->

---
layout: image
image: /vin-decode.jpg
title: VINs
---

<div class="abs-bl color-black ml-2 mb-1 text-xl">https://www.autocheck.com/vehiclehistory/vin-basics</div>

---

# Identifiers are information-rich

<ul>
<v-click><li>IDs often tell us the <u>location</u>, <u>time of creation</u> and <u>rate of change</u></li></v-click>
<v-click><li>IDs often represent real-world system limitations</li></v-click>
<v-click><li>Even a small sample set can define the range</li></v-click>
<v-click><li>Why does this matter?</li></v-click>
</ul>

<!--
  A single observation is often enough to make a guess
  Additional samples over time fill in the gaps
-->

---

# Missing ACLs are not just for the web

<ul class="mb-10">
<li>Insecure Direct Object References (IDOR), everywhere!</li>
<li>ID discovery enables data leaks and abuse</li>
</ul>

<div grid="~ cols-2 gap-2">

<v-click>
<img src="/walgreens.png" width="75%">
</v-click>

<v-click>
<img src="/chipotle.png" width="50%">
</v-click>

</div>

<!--

-->

---

# Business intelligence
<ul>
<li>Even minor leaks expose granular data over time</li>
<v-click><li>Oracle Commerce (ATG) DYN_USER_ID cookies</li></v-click>
</ul> 

<v-click>
<Transform scale="0.90">
<ATGCSV filePath="./atg.csv"/>
</Transform>
</v-click>

<!--

-->

---

# Application defense
<ul class="mb-10">
<li>Understanding identifiers is critical to security</li>
<li>Sequential? Predictable? Encoded?</li>
</ul> 

## Not always obvious...

<div class="font-mono mt-4">
<v-switch>

<template #1>
<ul>
<li>0x6716f208a5fb234a</li>
</ul>
</template>

<template #2>
<ul>
<li><span class="neonYellow">0x6716f208</span>a5fb234a</li>
<li><span class="neonYellow">1729557000</span></li>
<li><span class="neonGreen">2024-10-21 19:30:00 -0500</span></li>
</ul>
</template>

<template #3>
<ul>
<li>b0af43ac-0714-8f4c-ad77-f36f3f9daba4</li>
</ul>
</template>

<template #4>
<ul>
<li>b0af43ac-0714-8f4c-ad77-f36f3f9daba4</li>
<li><span class="neonYellow">ac43afb0-1407-4c8f</span>-ad77-f36f3f9daba4</li>
<li>SQL Server encoded UUID v4 (random)</li>
</ul>
</template>

<template #5>
<ul>
<li>ba209999-0c6c-11d2-97cf-00c04f8eea45</li>
</ul>
</template>

<template #6>
<ul>
<li>ba209999-0c6c-<span class="neonYellow">1</span>1d2-97<span class="neonYellow">c</span>f-<span class="neonYellow">00c04f8eea45</span></li>
<li>1998-06-25 20:40:26.586562.5 UTC</li>
<li>MAC Address <span class="neonGreen">00:c0:4f:8e:ea:45</span></li>
<li>UUID v1 (Dell Desktop)</li>
</ul>
</template>

</v-switch>
</div>

<!--

-->

---
title: Identifier Discovery
layout: section
---

# Identifier Discovery


---

# Discovery process

1. A sample identifier to seed discovery
1. An action to resolve an ID to attributes
1. A system to record the results
1. A method to correlate attributes

---

# Telephone networks

1. A sample identifier to seed discovery

<div class="ml-8 mt-2 mb-2 neonYellow">555-454-9600</div>

2. An action to resolve an ID to attributes

<div class="ml-8 mt-2 mb-2 neonYellow">Call the number and record the response</div>

3. A system to record the results

<div class="ml-8 mt-2 mb-2 neonYellow">A notebook</div>

4. A method to correlate attributes

<div class="ml-8 mt-2 mb-2 neonYellow">Link numbers with similar attributes</div>

---
layout: image
image: /modem.png
---

---

# 555-454-XXXX

<div grid="~ cols-2 gap-5">
<ul>
<li>10,000 numbers to a block</li>
</ul>
<Wardial gridID="emptyGrid" :grid-active=false :grid-steps=0></Wardial>
</div>

---

# 555-454-XXXX

<div grid="~ cols-2 gap-5">
<ul>
<li>10,000 numbers to a block</li>
<li>Each call takes 30 seconds</li>
</ul>
<Wardial gridID="slowGrid" :grid-active=true :grid-steps=1></Wardial>
</div>

---

# 555-454-XXXX

<div grid="~ cols-2 gap-5">
<ul>
<li>10,000 numbers to a block</li>
<li>Each call takes 30 seconds</li>
<li>83 hours to dial every line</li>
</ul>
<Wardial gridID="fastGrid" :grid-active=true :grid-steps=3></Wardial>
</div>

---

# 555-454-XXXX

<div grid="~ cols-2 gap-5">
<ul>
<li>10,000 numbers to a block</li>
<li>Each call takes 30 seconds</li>
<li>83 hours to dial every line</li>
<li>Patterns appear quickly</li>
</ul>
<Wardial gridID="turboGrid" :grid-active=true :grid-steps=25></Wardial>
</div>

---

# Discovery process (IPv4)

1. A sample identifier to seed discovery

<div class="ml-8 mt-2 mb-2 neonYellow">192.168.0.5</div>

2. An action to resolve an ID to attributes

<div class="ml-8 mt-2 mb-2 neonYellow">Scan the address for services and fingerprints</div>

3. A system to record the results

<div class="ml-8 mt-2 mb-2 neonYellow">A markdown file</div>

4. A method to correlate attributes

<div class="ml-8 mt-2 mb-2 neonYellow">Color addresses based on fingerprint</div>

---


# 192.168.0.0/24

<div grid="~ cols-2 gap-5">
<ul>
<li>256 numbers to a block</li>
</ul>

<div class="pl-12 mx-auto">

```mermaid {scale: 0.55, alt: 'A IPv4 /24 Subnet', theme: 'dark', darkMode: true}
block-beta
  columns 16
000 001 002 003 004 005 006 007 008 009 010 011 012 013 014 015 016 017 018 019 020 021 022 023 024 025 026 027 028 029 030 031 032 033 034 035 036 037 038 039 040 041 042 043 044 045 046 047 048 049 050 051 052 053 054 055 056 057 058 059 060 061 062 063 064 065 066 067 068 069 070 071 072 073 074 075 076 077 078 079 080 081 082 083 084 085 086 087 088 089 090 091 092 093 094 095 096 097 098 099 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
```
</div>
</div>


---


# 192.168.0.0/24

<div grid="~ cols-2 gap-5">
<ul>
<li>256 numbers to a block</li>
<li>Each IP takes a few seconds</li>
<li>A minute or so to scan every IP</li>
</ul>

<div class="pl-12 mx-auto">

```mermaid {scale: 0.55, alt: 'A IPv4 /24 Subnet', theme: 'dark', darkMode: true}
block-beta
  columns 16
000 001 002 003 004 005 006 007 008 009 010 011 012 013 014 015 016 017 018 019 020 021 022 023 024 025 026 027 028 029 030 031 032 033 034 035 036 037 038 039 040 041 042 043 044 045 046 047 048 049 050 051 052 053 054 055 056 057 058 059 060 061 062 063 064 065 066 067 068 069 070 071 072 073 074 075 076 077 078 079 080 081 082 083 084 085 086 087 088 089 090 091 092 093 094 095 096 097 098 099 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255

style 001 fill:#070
style 010 fill:#070
style 011 fill:#070
style 012 fill:#070
style 013 fill:#070
style 014 fill:#070
style 015 fill:#070
style 020 fill:#070
style 021 fill:#070
style 022 fill:#070
style 023 fill:#070
style 024 fill:#070
style 025 fill:#070
style 128 fill:#070
style 129 fill:#070
style 130 fill:#070
style 131 fill:#070
style 132 fill:#070
style 133 fill:#070
style 135 fill:#070
style 136 fill:#070
style 137 fill:#070
style 138 fill:#070
style 139 fill:#070
style 140 fill:#070
style 141 fill:#070
style 142 fill:#070
style 143 fill:#070
style 144 fill:#070
style 146 fill:#070
style 147 fill:#070
style 148 fill:#070
style 149 fill:#070
style 150 fill:#070
style 151 fill:#070
style 152 fill:#070
style 153 fill:#070
style 154 fill:#070
style 155 fill:#070
style 156 fill:#070
style 157 fill:#070
style 158 fill:#070
style 159 fill:#070
style 160 fill:#070
style 163 fill:#070
style 164 fill:#070
style 240 fill:#070
style 241 fill:#070
style 242 fill:#070
style 243 fill:#070
style 244 fill:#070
style 245 fill:#070
style 246 fill:#070
```

</div>
</div>


---


# 192.168.0.0/24

<div grid="~ cols-2 gap-5">
<ul>
<li>256 numbers to a block</li>
<li>Each IP takes a few seconds</li>
<li>A minute or so to scan every IP</li>
<li>Patterns also appear quickly</li>
</ul>

<div class="pl-12 mx-auto">
```mermaid {scale: 0.55, alt: 'A IPv4 /24 Subnet', theme: 'dark', darkMode: true}
block-beta
  columns 16
000 001 002 003 004 005 006 007 008 009 010 011 012 013 014 015 016 017 018 019 020 021 022 023 024 025 026 027 028 029 030 031 032 033 034 035 036 037 038 039 040 041 042 043 044 045 046 047 048 049 050 051 052 053 054 055 056 057 058 059 060 061 062 063 064 065 066 067 068 069 070 071 072 073 074 075 076 077 078 079 080 081 082 083 084 085 086 087 088 089 090 091 092 093 094 095 096 097 098 099 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255

style 001 fill:#077
style 010 fill:#070
style 011 fill:#700
style 012 fill:#700
style 013 fill:#700
style 014 fill:#700
style 015 fill:#700
style 020 fill:#070
style 021 fill:#990
style 022 fill:#990
style 023 fill:#990
style 024 fill:#990
style 025 fill:#990
style 128 fill:#070
style 129 fill:#707
style 130 fill:#707
style 131 fill:#707
style 132 fill:#707
style 133 fill:#707
style 135 fill:#990
style 136 fill:#707
style 137 fill:#707
style 138 fill:#707
style 139 fill:#707
style 140 fill:#707
style 141 fill:#707
style 142 fill:#707
style 143 fill:#707
style 144 fill:#707
style 146 fill:#707
style 147 fill:#707
style 148 fill:#707
style 149 fill:#707
style 150 fill:#707
style 151 fill:#707
style 152 fill:#707
style 153 fill:#707
style 154 fill:#707
style 155 fill:#707
style 156 fill:#707
style 157 fill:#707
style 158 fill:#707
style 159 fill:#707
style 160 fill:#707
style 163 fill:#707
style 164 fill:#707
style 240 fill:#070
style 241 fill:#659
style 242 fill:#659
style 243 fill:#659
style 244 fill:#659
style 245 fill:#659
style 246 fill:#659

```

<div grid="~ cols-6 gap-1" class="text-xs text-center legend">
<div class="legRouter">Router</div>
<div class="legSwitch">Switch</div>
<div class="legServer">Server</div>
<div class="legPrinter">Printer</div>
<div class="legEndpoint">Endpoint</div>
<div class="legCamera">Camera</div>
</div>

</div>
</div>


---

# Enterprise internal

<img src="/subnet-int.png" width="85%">


---

# Public IPv4

<div grid="~ cols-2 gap-5">
<img src="/subnet-ext.png" width="100%">
<div>
<img src="/subnet-ext.png" width="50%" class="mb-5">
<img src="/subnet-ext.png" width="25%">
</div>
</div>


---
layout: image
image: /ipv4_map.png
---


---
layout: image
image: /ipv4_hilbert.png
---

<div class="abs-br font-bold color-white mr-3 text-sm">https://hdm.io/decks/UNITED_2015_Internet_of_Threats_A.pdf</div>


---

# IPv4 is full, go home

<div grid="~ cols-2 gap-10" class="mt-20">
<div class="text-center text-xl border-rounded p-5 border-1">
  <div class="text-4xl neonYellow mb-3 text-center">
    3.7b of 4.3b
  </div>
  of IPv4 is routable
</div>
<div class="text-center text-xl border-rounded p-5 border-1">
  <div class="text-4xl neonPink mt-5 mb-3 text-center">
    774m of 3706m
  </div>
  is already in Shodan
</div>
</div>

<div grid="~ cols-3 gap-10" class="mt-15">

<div/>
<div class="text-center text-xl border-rounded p-5 border-1">
  <div class="text-4xl neonGreen mt-5 mb-3 text-center">
    17% chance
  </div>
  of any IPv4 being live
</div>

<div/>
</div>

---

# IPv6 is the opposite (128 bits)

* Every host gets IPv4 ^ ² addresses
* Range-based discovery doesn't work

<div grid="~ cols-3 gap-5" class="mt-3">
<img src="/ipv6_hilbert.png" width="100%">
<div>
<img src="/ipv6_hilbert_zoom1.png" width="100%">
</div>
<div>
<img src="/ipv6_hilbert_zoom2.png" width="100%">
</div>
</div>

<div class="abs-br font-bold color-white mr-50 mb-3 text-sm">https://observablehq.com/@vasturiano/hilbert-map-of-ipv6-address-space</div>



---
layout: iframe
url: https://esahubble.org/images/heic1502a/zoomable/
---

---


# IPv6 link-local

* Local IPv6 discovery is trivial
```console
sh-3.2# ping6 ff02::1%en0

PING6(56=40+8+8 bytes) fe80::bd:7caa:2daa:c6b8%en0 --> ff02::1%en0
16 bytes from fe80::bd:7caa:2daa:c6b8%en0, icmp_seq=0 hlim=64 time=6.111 ms
16 bytes from fe80::f6e2:c6ff:fea8:ca34%en0, icmp_seq=0 hlim=64 time=12.431 ms
16 bytes from fe80::76ac:b9ff:fe5b:eca4%en0, icmp_seq=0 hlim=64 time=16.818 ms
16 bytes from fe80::f690:eaff:fe00:823f%en0, icmp_seq=0 hlim=64 time=20.237 ms
16 bytes from fe80::1c5a:a22:eac6:bf31%en0, icmp_seq=0 hlim=64 time=22.755 ms
16 bytes from fe80::d217:69ff:feb0:cf03%en0, icmp_seq=0 hlim=64 time=112.749 ms
16 bytes from fe80::eac7:4fff:fe04:c4ea%en0, icmp_seq=0 hlim=64 time=211.174 ms
16 bytes from fe80::fa0f:f9ff:fe87:b909%en0, icmp_seq=0 hlim=64 time=212.109 ms
16 bytes from fe80::5660:9ff:fe9e:f9ea%en0, icmp_seq=0 hlim=64 time=217.347 ms
16 bytes from fe80::1042:8d8d:771b:3535%en0, icmp_seq=0 hlim=64 time=241.916 ms
16 bytes from fe80::4661:32ff:fe12:494f%en0, icmp_seq=0 hlim=64 time=242.435 ms
16 bytes from fe80::d6f5:47ff:fe21:fc1%en0, icmp_seq=0 hlim=64 time=242.821 ms
16 bytes from fe80::4661:32ff:fe1d:4d79%en0, icmp_seq=0 hlim=64 time=254.185 ms
16 bytes from fe80::10b6:ff9a:de65:8e87%en0, icmp_seq=0 hlim=64 time=263.771 ms
16 bytes from fe80::1c8d:ddec:c48a:5721%en0, icmp_seq=0 hlim=64 time=264.057 ms

```


---

# Public IPv6 is an art

<img src="/hitlist_1.png" width="90%">

<div class="abs-bl font-bold color-white ml-3 mb-2 text-lg">https://ipv6hitlist.github.io/</div>

---

# IPv6 hitlist results

<img src="/hitlist_2.png" width="90%">

<div class="abs-bl font-bold color-white ml-3 mb-2 text-lg">https://ipv6hitlist.github.io/</div>

---

# Shodan wins!

<img src="/shodan_ipv6.png" width="85%">

<div class="abs-bl font-bold color-white ml-30 mb-2 text-lg">https://www.shodan.io/search?query=has_ipv6%3Atrue</div>


---
title: Universally unique identifiers
---

# Universally unique identifiers

<div class="font-mono font-bold mb-3 text-3xl neonGreen">1ef7e299-fa25-4f65-afca-ee27cc61b843</div>

* 128 bits, like IPv6, multiple versions, and everywhere
* Random-looking, but often richly encoded


---
title: UUID versions
---

# UUID versions

<div class="text-2xl font-mono">

<div><span class="neonBlue">v1:</span> <span class="neonYellow">f270fa6e</span><span class="neonYellow">-9214</span>-<span class="neonGreen">1</span><span class="neonYellow">1ef-</span><span class="neonGreen">b</span><span class="neonYellow">864-</span><span class="neonOrange">00c04f8eea45</span></div>

<div><span class="neonBlue">v2:</span> <span class="neonYellow">000003e8</span><span class="neonYellow">-921b</span>-<span class="neonGreen">2</span><span class="neonYellow">1ef-</span><span class="neonGreen">9</span><span class="neonYellow">400-</span><span class="neonOrange">325096b39f47</span></div>

<div><span class="neonBlue">v3:</span> <span class="neonPink">3a232406-35ad-</span><span class="neonGreen">3</span><span class="neonPink">9bb</span>-<span class="neonGreen">8</span><span class="neonPink">b78-3b7b3624a768</span></div>

<div><span class="neonBlue">v4:</span> 9c5b94b1-35ad-<span class="neonGreen">4</span>9bb-<span class="neonGreen">b</span>118-8e8fc24abf80</div>

<div><span class="neonBlue">v5:</span> <span class="neonPink">da81c735-c250-</span><span class="neonGreen">5</span><span class="neonPink">8bc</span>-<span class="neonGreen">b</span><span class="neonPink">407-89ecef772215</span></div>

<div><span class="neonBlue">v6:</span> <span class="neonYellow">1e65ced7-cdcb</span>-<span class="neonGreen">6</span><span class="neonYellow">79d-</span><span class="neonGreen">8</span><span class="neonYellow">405-</span><span class="neonOrange">c8bcc8a0b1fd</span></div>

<div><span class="neonBlue">v7:</span> <span class="neonYellow">0192bf28-cf17-</span><span class="neonGreen">7</span><span class="color-white">2f6-</span><span class="neonGreen">a</span><span class="color-white">0ee-c48769f6a408</span></div>

<div><span class="neonBlue">v8:</span> <span class="color-gray">9c5b94b1-35ad-</span><span class="neonGreen">8</span><span class="color-gray">9bb-</span><span class="neonGreen">b</span><span class="color-gray">118-8e8fc24abf80</span></div>
</div>

<div grid="~ cols-3 gap-1" class="mt-10 text-base font-bold">
<div class="neonGreen">Version/Variant</div>
<div class="neonYellow">Timestamp</div>
<div class="neonOrange">MAC/Node</div>
<div class="neonPink">MD5/SHA</div>
<div class="color-white">Random</div>
<div class="color-gray">Vendor</div>
</div>


---

# Sources of UUIDs

* Web requests (BurpSuite + UUID Detector¹)
* Microsoft Office file formats (docID)
* Windows registry & binaries
* Database record IDs

<div class="abs-bl font-bold color-white ml-3 mb-2 text-lg">1. https://github.com/PortSwigger/uuid-detector</div>


---

# Windows registry

* Dump all UUID/GUIDs from the Windows registry
* Extract UUID v1/v2 nodes, convert to MACs

<Transform scale="0.90">
<WinReg filePath="./reg.json"/>
</Transform>

---

# UUID v7 adoption

* UUID v4 effectively replaced UUID v1
* UUID v4 isn't great for sharding
* UUID v7 helps, but at a cost
* 48-bit ts with ms precision
* Expect to see it soon!

<div class="font-mono font-bold mt-10">
<div><span class="neonYellow">0192bf28-cf17-</span><span class="neonGreen">7</span><span class="color-white">2f6-</span><span class="neonGreen">a</span><span class="color-white">0ee-c48769f6a408</span></div>
</div>

<div class="abs-bl font-bold color-white ml-20 mb-3 text-xs">https://aws.amazon.com/blogs/database/implement-uuidv7-in-amazon-rds-for-postgresql-using-trusted-language-extensions/</div>



---

# MAC addresses
 
  * Associated with Ethernet, WiFi, & Bluetooth
  * 48-bits (6 bytes), but prefix-allocated
  * Currently ~53,000 prefixes
  * Prefix lengths vary

<div class="ml-10">
<div class="font-mono font-bold mt-4 text-3xl"><span class="neonYellow">30:20:4b</span><span class="color-white">:00:01:02</span> (L)</div>
<div class="font-mono font-bold mt-4 text-3xl"><span class="neonYellow">18:c3:f4:1</span><span class="color-white">0:01:02</span> (M)</div>
<div class="font-mono font-bold mt-4 text-3xl"><span class="neonYellow">00:1b:c5:00:4</span><span class="color-white">0:02</span> (S)</div>
</div>

---

# MAC history
 
* Companies (and people) purchase a prefix from IEEE
* As devices are shipped, new prefixes are added
* IEEE records the owner & address
* Historical data requires work
  * https://github.com/hdm/mac-ages/

<div class="font-mono font-bold mt-10 text-3xl"><span class="neonYellow">30:20:4b</span><span class="color-white">:00:01:02</span></div>
<div class="mt-3">Huawei on <span class="neonGreen">2024-10-23</span></div>


---

# Data mining MACs

* MACs are exposed via SNMP, mDNS, NetBIOS, and more
* Sometimes via unlikely avenues
* Odd scan on ports 987 & 9302

```
SRCH * HTTP/1.1
device-discovery-protocol-version:00030010
```


---

# PlayStations!

```
{
  "type": "result",
  "ts": 1729755767731551726,
  "host": "141.41.34.20",
  "port": "9302",
  "proto": "udp",
  "probe": "psdisco",
  "info": {
    "psdisco.code": "200",
    "psdisco.id": "5C96669DAB01",
    "psdisco.name": "PS5-912",
    "psdisco.protoVersion": "00030010",
    "psdisco.requestPort": "997",
    "psdisco.status": "Ok",
    "psdisco.sysVersion": "10010000",
    "psdisco.type": "PS5"
  }
}
```

* The ID `5C96669DAB01` looks familiar...

---

# PlayStations MACs

<div class="font-mono font-bold mt-10 text-3xl"><span class="neonYellow">5C:96:66:9D:AB:01</span></div>
<div class="mt-3">Sony Interactive Entertainment on <span class="neonGreen">2021-08-27</span></div>

---

# PlayStation status

<div grid="~ cols-2 gap-10" class="mt-20">

<div>

## Firmware

<div class="mt-3 font-mono text-xs"/>
<pre class="text-xs">43288 10200006
33216 12008011
2765 10010000
2397 11520011
1606 11508011
694 11020001
367 11008001
311 09008031
279 10508011
177 10010001
172 09600004
135 10710001
90 10000046
63 09600011
54 09030001
37 09400008
33 06720001
29 09200005

</pre>
</div>
<div>

## Applications

<div class="mt-3 font-mono text-xs"/>
<pre class="text-xs">2466 YouTube
615 Netflix
354 Call of Duty®
303 Fortnite
285 Prime Video
243 EA SPORTS FC 25
176 Grand Theft Auto V
129 Apex Legends
123 Disney+
120 eFootball™
102 Twitch
99 Hulu
93 原神
78 Max
69 Red Dead Redemption 2
68 Overwatch 2
60 TubiTV
60 Crunchyroll
</pre>

</div>
</div>


---

# Summary

* Short identifiers are pervasive and dangerous

* Long identifiers provide precise tracking

* Fun data is everywhere!


---
layout: cover
class: text-center
---
#  Thank you!

<div class="text-2xl mt-10">
  <span class="neonBlue">hdm</span> @ <span class="neonYellow">runZero.com</span>
</div>

 <div class="abs-tl m-5 flex gap-2 opacity-85">
  <img src="/lascon.png" width="200px">
</div>

<div class="abs-tr m-5 flex gap-2 opacity-85">
 <img src="/runzero.svg" width="200px">
</div>
