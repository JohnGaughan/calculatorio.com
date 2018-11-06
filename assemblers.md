---
layout: default
title: Assemblers
navigation_weight: 50
permalink: /assemblers/
---

## Item production rate

When using beacons and modules, ratios can get a bit wonky. It helps to normalize this by figuring out how many items a particular group of assembling machines produce per unit time, as well as how many multiples of their inputs are consumed in that unit time: due to productivity bonuses, the two do not always match.

Crafting speed and productivity come from the in-game UI.

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
