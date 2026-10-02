---
layout: default
title: Documentation
lang: en
permalink: /en/dokumantasyon
translation_url: /dokumantasyon
---

# Documentation

I collect my setup, configuration, and usage notes on enterprise tools here.

{% assign dokumanlar = site.posts | where: "lang", "en" | where: "categories", "dokumantasyon" | sort: "order" %}

{% if dokumanlar.size == 0 %}
<p>Posts about JumpCloud and Trend Micro are coming soon. 🌸</p>
{% else %}
{% assign gruplar = dokumanlar | group_by: "tool" %}
{% assign grup_isimleri = gruplar | map: "name" %}
<div class="doc-tabs">
  <div class="doc-tab-buttons">
    {% for grup in gruplar %}
      <button type="button" class="doc-tab-btn{% if forloop.first %} active{% endif %}" data-tab="doc-tab-{{ grup.name | slugify }}">{{ grup.name }}</button>
    {% endfor %}
    {% unless grup_isimleri contains "Trend Micro" %}
      <button type="button" class="doc-tab-btn" data-tab="doc-tab-trend-micro">Trend Micro</button>
    {% endunless %}
  </div>
  <div class="doc-tab-content">
    {% for grup in gruplar %}
      {% assign tool_slug = grup.name | slugify %}
      <div class="doc-tab-panel{% if forloop.first %} active{% endif %}" id="doc-tab-{{ tool_slug }}">
        {% assign walkthrough_items = grup.items | where_exp: "item", "item.doc_type != 'troubleshooting'" %}
        {% assign troubleshooting_items = grup.items | where: "doc_type", "troubleshooting" %}
        {% if troubleshooting_items.size > 0 %}
          <div class="doc-tabs doc-tabs-sub">
            <div class="doc-tab-buttons">
              <button type="button" class="doc-tab-btn active" data-tab="doc-subtab-{{ tool_slug }}-walkthrough">Documentation</button>
              <button type="button" class="doc-tab-btn" data-tab="doc-subtab-{{ tool_slug }}-troubleshooting">Troubleshooting</button>
            </div>
            <div class="doc-tab-content">
              <div class="doc-tab-panel active" id="doc-subtab-{{ tool_slug }}-walkthrough">
                {% include solution-list.html posts=walkthrough_items %}
              </div>
              <div class="doc-tab-panel" id="doc-subtab-{{ tool_slug }}-troubleshooting">
                {% include solution-list.html posts=troubleshooting_items %}
              </div>
            </div>
          </div>
        {% else %}
          {% include solution-list.html posts=walkthrough_items %}
        {% endif %}
      </div>
    {% endfor %}
    {% unless grup_isimleri contains "Trend Micro" %}
      <div class="doc-tab-panel" id="doc-tab-trend-micro">
        <p>Posts about Trend Micro are coming soon. 🌸</p>
      </div>
    {% endunless %}
  </div>
</div>
{% endif %}
