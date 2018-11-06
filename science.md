---
layout: calculator
title: Science
navigation_weight: 70
permalink: /science/
factorio_version: 0.16.51
---

## Assemblers required for a given science per minute

If your target is X science per minute, this will tell you how many assemblers you need for each science pack given particular bonuses for speed and productivity. Defaults assume speed 3 modules in eight beacons near each assembler, with four productivity 3 modules in assembler 3s.

Crafting speed and productivity come from the in-game UI.

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

## Science lab consumption of science packs

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

