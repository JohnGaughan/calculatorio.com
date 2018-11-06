---
layout: default
title: Mining
navigation_weight: 30
permalink: /mining/
---

## Electric mining drills required to saturate a belt

Given a resource patch of a certain type and a specified level of mining productivity research, how many electric mining drills are required to saturate the entire belt?

The first number is the calculated number for the entire belt, but is likely a fraction and not practical. The second number is divided by two and rounded up, giving an integer number of drills to put on each side.

<div class="inputs">
<div class="input-row">
<div class="input-label">Belt tier:</div>
<div class="input">
<select id="drillsPerBeltTier">
<option value="13.33">Yellow</option>
<option value="26.67">Red</option>
<option value="40">Blue</option>
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Material being mined:</div>
<div class="input">
<select id="drillsPerBeltMaterial">
<option value="0.525">Coal, Iron, Copper</option>
<option value="0.65">Stone</option>
<option value="0.2625">Uranium</option>
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
<option value="13.33">Yellow</option>
<option value="26.67">Red</option>
<option value="40">Blue</option>
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Material being mined:</div>
<div class="input">
<select id="beltsPerPatchMaterial">
<option value="0.525">Coal, Iron, Copper</option>
<option value="0.65">Stone</option>
<option value="0.2625">Uranium</option>
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
