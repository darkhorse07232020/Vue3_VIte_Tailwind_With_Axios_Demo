# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)


There are three 3rd party API endpoints.
If you set the HTTP request headers to "Accept: application/json" and "Content-Type: application/json" then API will return the data in JSON format.
First endpoint to get all the available vehicle years:
GET http://new.api.nexusautotransport.com/api/vehicles/years
Second endpoint to get all the available vehicle makes for a given year (change the URL parameter 'year'):
GET http://new.api.nexusautotransport.com/api/vehicles/makes?year=2020
Third endpoint to get all the available vehicle models for a given year/make (change the URL parameters 'year' and 'make'):
GET http://new.api.nexusautotransport.com/api/vehicles?year=2021&vehicle_make_id=35
Your task, using Vue.js, is to create a dynamic dropdown for selecting Year/Make/Model with data taken from the API.
