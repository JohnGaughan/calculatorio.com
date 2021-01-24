---
layout: calculator
title: Science
navigation_weight: 70
permalink: /science/
factorio_version: 0.16.51
---

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

