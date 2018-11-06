---
layout: calculator
title: Mining
navigation_weight: 30
permalink: /mining/
factorio_version: 0.16.51
---

## Electric mining drills required to saturate a belt

Given a resource patch of a certain type and a specified level of mining productivity research, how many electric mining drills are required to saturate the entire belt?

The first number is the calculated number for the entire belt, but is likely a fraction and not practical. The second number is divided by two and rounded up, giving an integer number of drills to put on each side.

<div class="inputs">
<div class="input-row">
<div class="input-label">Belt tier:</div>
<div class="input">
<select id="drillsPerBeltTier">
{% for belt in site.data.belt %}
<option value="{{ belt.speed }}">{{ belt.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Material being mined:</div>
<div class="input">
<select id="drillsPerBeltMaterial">
{% for ore in site.data.ore %}
<option value="{{ ore.hardness }}">{{ ore.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Productivity research level:</div>
<div class="input"><input type="text" id="drillsPerBeltProd" value="0" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Drills:</div>
<div class="input"><input type="text" id="drillsPerBelt" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Put this many drills on each side of the belt:</div>
<div class="input"><input type="text" id="drillsPerLane" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div><button onclick="calculateDrillsPerBelt();">Calculate</button></div>
</div>
</div>
<script>
function calculateDrillsPerBelt() {
var p = 1 + 2 * Number(document.getElementById("drillsPerBeltProd").value) / 100;
var drills = Number(document.getElementById("drillsPerBeltTier").value) / (Number(document.getElementById("drillsPerBeltMaterial").value) * p);
document.getElementById("drillsPerBelt").value = drills.toFixed(2);
var perLane = 0.5 + drills / 2;
document.getElementById("drillsPerLane").value = perLane.toFixed(0);
}
</script>

## Belts for a given number of drills on an ore patch

When cramming as many drills as possible into an ore patch, some of the belt lines might not have enough drills to compress the belt. Perhaps you have five belts coming from the ore patch, but only enough ore to saturate two belts. It helps to know exactly how many belts can be compressed to avoid building extra lines of belts and furnaces for maximum efficiency. This is crucial in the early game when resources are scarce, because you are in the process of setting up your production lines. In the previous example, it would make sense to use a 5-to-2 belt balancer (reducer) to shrink the number of belts, saving resources.

This calculator is a sort-of inverse of the one above that tells you how many drills you need. This one takes the number of drills on each side of the belt, and tells you how many belts' worth of ore it will produce for each lane (left and right). If the two lanes are more than a little bit uneven, it may be worth redirecting some ore output onto the opposite lane.

<div class="inputs">
<div class="input-row">
<div class="input-label">Belt tier:</div>
<div class="input">
<select id="beltsPerPatchTier">
{% for belt in site.data.belt %}
<option value="{{ belt.speed }}">{{ belt.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Material being mined:</div>
<div class="input">
<select id="beltsPerPatchMaterial">
{% for ore in site.data.ore %}
<option value="{{ ore.hardness }}">{{ ore.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Productivity research level:</div>
<div class="input"><input type="text" id="beltsPerPatchProd" value="0" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Drills feeding left lane:</div>
<div class="input"><input type="text" id="drillsPerBeltLeft" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Drills feeding right lane:</div>
<div class="input"><input type="text" id="drillsPerBeltRight" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Belts of output in the left lane:</div>
<div class="input"><input type="text" id="drillsPerBeltLeftThroughput" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Belts of output in the right lane:</div>
<div class="input"><input type="text" id="drillsPerBeltRightThroughput" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div><button onclick="calculateBeltsPerPatch();">Calculate</button></div>
</div>
</div>
<script>
function calculateBeltsPerPatch() {
var p = 1 + 2 * Number(document.getElementById("beltsPerPatchProd").value) / 100;
var drillsPerBelt = Number(document.getElementById("beltsPerPatchTier").value) / (Number(document.getElementById("beltsPerPatchMaterial").value) * p);
var beltsLeft = document.getElementById("drillsPerBeltLeft").value / drillsPerBelt;
var beltsRight = document.getElementById("drillsPerBeltRight").value / drillsPerBelt;
document.getElementById("drillsPerBeltLeftThroughput").value = beltsLeft.toFixed(2);
document.getElementById("drillsPerBeltRightThroughput").value = beltsRight.toFixed(2);
}
</script>

## Mining productivity breakpoints for electric mining drills on belts

When researching mining productivity, not every level of research will affect the number of drills needed to compress a belt of ore. Just in case you are contemplating starting that next level of research before bed but are not sure if it will have a meaningful impact on the number of drills per belt, this calculator will tell you the breakpoints.

Please note that this calculator determines the number of drills _per side_ of the belt, since that is the practical application. If it takes 27 drills to saturate a belt, few people will bother concocting a way to have that odd-drill-out alternate belt lanes.

<div class="inputs">
<div class="input-row">
<div class="input-label">Belt tier:</div>
<div class="input">
<select id="prodBreakpointsTier">
{% for belt in site.data.belt %}
<option value="{{ belt.speed }}">{{ belt.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Material being mined:</div>
<div class="input">
<select id="prodBreakpointsMaterial">
{% for ore in site.data.ore %}
<option value="{{ ore.hardness }}">{{ ore.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div><button onclick="calculateProdBreakpoints();">Calculate</button></div>
</div>
</div>
<div class="table" id="prodBreakpointsOutput"></div>
<script>
function calculateProdBreakpoints() {

var html = '<div class="table-header"><div class="table-cell">Productivity Level</div><div class="table-cell">Drills Per Side</div></div>';

var beltSpeed = document.getElementById("prodBreakpointsTier").value;
var hardness = document.getElementById("prodBreakpointsMaterial").value;

var prod = 0;
var previousDrills = -1;
while (previousDrills != 1) {
var drills = Math.ceil((beltSpeed) / (hardness * (1 + 2 * prod / 100)) / 2);
if (drills != previousDrills) {
html += '<div class="table-row"><div class="table-cell">' + prod + '</div><div class="table-cell">' + drills + '</div></div>';
previousDrills = drills;
}
++prod;
}
document.getElementById("prodBreakpointsOutput").innerHTML = html;
}
</script>
