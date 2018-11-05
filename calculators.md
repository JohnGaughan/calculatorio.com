---
layout: default
title: Calculators
navigation_weight: 50
permalink: /calculators/
---

## Factorio Reference

The calculators in this page are valid for Factorio version 0.16. Factorio 0.17 is [confirmed to alter some of the data](https://www.factorio.com/blog/post/fff-266) used in the calculators. If you are reading this message after 0.17 is released but before I update the calculators and edit this intro, keep in mind that some of them may produce incorrect results.

All calculations are driven by client-side JavaScript, which must be enabled for them to work.

Any time an input box requests the speed of a machine, hover over it in-game and use the value provided by the game's UI. This takes into account the base speed of the machine, any speed upgrades, modules, and beacons. Productivity is expressed as a percentage in-game, and should be entered as a decimal here. Base productivity is 1, 40% bonus is 1.4.

### Electric mining drills required to saturate a belt

Given a resource patch of a certain type and a specified level of mining productivity research, how many electric mining drills are required to saturate the entire belt? Please note that drills are unlikely to <em>compress</em> a belt without additional effort.

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

### Item production rate

When using beacons and modules, ratios can get a bit wonky. It helps to normalize this by figuring out how many items a particular group of assembling machines produce per unit time, as well as how many multiples of their inputs are consumed in that unit time: due to productivity bonuses, the two do not always match.

<div class="inputs">
<div class="input-row">
<div class="input-label">Number of machines:</div>
<div class="input"><input type="text" id="itemProductionRateMachines" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Yield per craft:</div>
<div class="input"><input type="text" id="itemProductionRateYield" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Crafting speed:</div>
<div class="input"><input type="text" id="itemProductionRateSpeed" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Productivity:</div>
<div class="input"><input type="text" id="itemProductionRateProd" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Base recipe speed:</div>
<div class="input"><input type="text" id="itemProductionRateBaseSpeed" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Units produced per second:</div>
<div class="input"><input type="text" id="itemProductionRateProdSec" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Units produced per minute:</div>
<div class="input"><input type="text" id="itemProductionRateProdMin" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Inputs consumed per second:</div>
<div class="input"><input type="text" id="itemProductionRateConsumeSec" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Inputs consumed per minute:</div>
<div class="input"><input type="text" id="itemProductionRateConsumeMin" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div class="input"><button onclick="calculateItemProductionRate();">Calculate</button></div>
</div>
</div>
<script>
function calculateItemProductionRate() {
var machines = Number(document.getElementById("itemProductionRateMachines").value);
var yield = Number(document.getElementById("itemProductionRateYield").value);
var speed = Number(document.getElementById("itemProductionRateSpeed").value);
var productivity = Number(document.getElementById("itemProductionRateProd").value);
var baseSpeed = Number(document.getElementById("itemProductionRateBaseSpeed").value);
var producedPerSecond = machines * yield * speed * productivity / baseSpeed;
var producedPerMinute = 60 * producedPerSecond;
var consumedPerSecond = machines * speed / baseSpeed;
var consumedPerMinute = 60 * consumedPerSecond;
document.getElementById("itemProductionRateProdSec").value = producedPerSecond.toFixed(2);
document.getElementById("itemProductionRateProdMin").value = producedPerMinute.toFixed(2);
document.getElementById("itemProductionRateConsumeSec").value = consumedPerSecond.toFixed(2);
document.getElementById("itemProductionRateConsumeMin").value = consumedPerMinute.toFixed(2);
}
</script>

### Assemblers required for a given science per minute

If your target is X science per minute, this will tell you how many assemblers you need for each science pack given particular bonuses for speed and productivity. Defaults assume speed 3 modules in eight beacons near each assembler, with four productivity 3 modules in assembler 3s.

<div class="inputs">
<div class="input-row">
<div class="input-label">Desired science per minute:</div>
<div class="input"><input type="text" id="spmIn" value="1000" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Crafting speed:</div>
<div class="input"><input type="text" id="spmSpeed" value="5.5" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Productivity:</div>
<div class="input"><input type="text" id="spmProd" value="1.4" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Assemblers, red science packs:</div>
<div class="input"><input type="text" id="spmRed" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Assemblers, green science packs:</div>
<div class="input"><input type="text" id="spmGreen" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Assemblers, blue science packs:</div>
<div class="input"><input type="text" id="spmBlue" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Assemblers, military science packs:</div>
<div class="input"><input type="text" id="spmMilitary" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Assemblers, production science packs:</div>
<div class="input"><input type="text" id="spmProduction" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Assemblers, high tech science packs:</div>
<div class="input"><input type="text" id="spmHighTech" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div class="input"><button onclick="calculateSpmAssemblers();">Calculate</button></div>
</div>
</div>
<script>
function calculateSpmAssemblers() {
var targetSpm = Number(document.getElementById("spmIn").value);
var speed = Number(document.getElementById("spmSpeed").value);
var productivity = Number(document.getElementById("spmProd").value);

var red = 5 * targetSpm / (60 * speed * productivity);
var green = 6 * targetSpm / (60 * speed * productivity);
var blue = 12 * targetSpm / (60 * speed * productivity);
var black = 10 * targetSpm / (60 * 2 * speed * productivity);
var purple = 14 * targetSpm / (60 * 2 * speed * productivity);
var yellow = 14 * targetSpm / (60 * 2 * speed * productivity);

document.getElementById("spmRed").value = red.toFixed(2);
document.getElementById("spmGreen").value = green.toFixed(2);
document.getElementById("spmBlue").value = blue.toFixed(2);
document.getElementById("spmMilitary").value = black.toFixed(2);
document.getElementById("spmProduction").value = purple.toFixed(2);
document.getElementById("spmHighTech").value = yellow.toFixed(2);
}
</script>

### Science lab consumption of science packs

Megabases are measured in how many science packs they both produce and consume per minute. It is important to balance production and consumption. Most infinite research tasks require a base of 60 seconds. However, some require less. Check the research UI in game. Lab speed and productivity are provided by the game's UI when hovering over a science lab and includes lab speed upgrades.

<div class="inputs">
<div class="input-row">
<div class="input-label">Science lab speed (+X%):</div>
<div class="input"><input type="text" id="scienceLabSpmSpeed" value="0" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Research base time:</div>
<div class="input"><input type="text" id="scienceLabSpmBaseTime" value="60" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Number of labs:</div>
<div class="input"><input type="text" id="scienceLabSpmLabs" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Science consumed per minute:</div>
<div class="input"><input type="text" id="scienceLabSpm" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div><button onclick="calculateScienceConsumedPerMinute();">Calculate</button></div>
</div>
</div>
<script>
function calculateScienceConsumedPerMinute() {
var speedDivisor = (Number(document.getElementById("scienceLabSpmSpeed").value) + 100) / 100;
var researchTime = Number(document.getElementById("scienceLabSpmBaseTime").value) / speedDivisor;
var perSecond = 1 / researchTime;
var totalPerSecond = Number(document.getElementById("scienceLabSpmLabs").value) * perSecond;
var totalPerMinute = 60 * totalPerSecond;
document.getElementById("scienceLabSpm").value = totalPerMinute.toFixed(2);
}
</script>

