---
layout: calculator
title: Train Acceleration
navigation_weight: 80
permalink: /train_acceleration/
factorio_version: 0.16.51
---

## Train acceleration and top speed

Trains accelerate faster or slower based on their mass, air resistance of the wagon in front (usually a locomotive but it can be anything), and total number of wagons, including locomotives. Furthermore, the top speed varies based on the fuel used.

This calculator lets you define all of the relevant information about your train and determine its top speed, as well as precisely how long it takes to reach that top speed.


<div class="inputs">
<div class="input-row">
<div class="input-label">Number of forward-facing locomotives:</div>
<div class="input"><input type="text" id="forward_locomotives" value="1" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Number of backward-facing locomotives:</div>
<div class="input"><input type="text" id="backward_locomotives" value="0" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Number of cargo and fluid wagons:</div>
<div class="input"><input type="text" id="cargo_fluid_wagons" value="0" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Number of artillery wagons:</div>
<div class="input"><input type="text" id="artillery_wagons" value="0" size="3"/></div>
</div>
<div class="input-row">
<div class="input-label">Type of wagon in front of the train:</div>
<div class="input">
<select id="front_wagon">
{% for wagon in site.data.wagon %}
<option value="{{ wagon.air_resistance }}">{{ wagon.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Fuel type:</div>
<div class="input">
<select id="fuel">
{% for fuel in site.data.fuel %}
<option value="{{ fuel.acceleration }},{{ fuel.top_speed }}">{{ fuel.name }}</option>
{% endfor %}
</select>
</div>
</div>
<div class="input-row">
<div class="input-label">Number of seconds required to reach top speed:</div>
<div class="input"><input type="text" id="time" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label">Top speed in km/h:</div>
<div class="input"><input type="text" id="velocity" disabled="" readonly="" size="5"/></div>
</div>
<div class="input-row">
<div class="input-label"></div>
<div><button onclick="calculateScienceConsumedPerMinute();">Calculate</button></div>
</div>
</div>
<script>
function calculateScienceConsumedPerMinute() {
var forward_locomotives = Number(document.getElementById("forward_locomotives").value);
var backward_locomotives = Number(document.getElementById("backward_locomotives").value);
var cargo_fluid_wagons = Number(document.getElementById("cargo_fluid_wagons").value);
var artillery_wagons = Number(document.getElementById("artillery_wagons").value);
var fuel = document.getElementById("fuel").value.split(",");
var fuel_acceleration_bonus = Number(fuel[0]);
// Base top speed is 1.2 meters per tick
var max_speed = 1.2 * Number(fuel[1]);
var air_resistance_of_front_rolling_stock = Number(document.getElementById("front_wagon").value);
var train_weight = 2000 * (forward_locomotives + backward_locomotives) + 1000 * cargo_fluid_wagons + 4000 * artillery_wagons;
var train_friction_force = (forward_locomotives + backward_locomotives + cargo_fluid_wagons + artillery_wagons) / 2;
var old_train_speed = -1;
var train_speed = 0;
var resistance = (1 - air_resistance_of_front_rolling_stock * 1000 / train_weight);
var acceleration = (10 * forward_locomotives * fuel_acceleration_bonus / train_weight) - (train_friction_force / train_weight);
var ticks = 0;
if (acceleration < 0) {
 acceleration = 0;
}
if (acceleration > 0) {
 while (train_speed != old_train_speed) {
  old_train_speed = train_speed;
  train_speed = (old_train_speed + acceleration) * resistance;
  train_speed = Math.min(max_speed, train_speed);
  train_speed = Math.max(0, train_speed);
  ++ticks;
 }
}
// Speed is measured in tiles (meters) per tick. Multiply by 60 to get m/s, then 3.6 to get km/h
train_speed = train_speed * 60 * 3.6;
var time = ticks / 60;
document.getElementById("time").value = time.toFixed(2);
document.getElementById("velocity").value = train_speed.toFixed(2);
}
</script>
