---
title: Matplotlib速查
authors: Ethan Lin
year: 2023-03-31 
tags:
  - 日期/2023-03-31 
  - 类型/笔记 
---


# Matplotlib速查






## Artist对象之属性

Every Matplotlib `Artist` has the following properties

| Property   | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| alpha      | The transparency - a scalar from 0-1                         |
| animated   | A boolean that is used to facilitate animated drawing        |
| axes       | The Axes that the Artist lives in, possibly None             |
| clip_box   | The bounding box that clips the Artist                       |
| clip_on    | Whether clipping is enabled                                  |
| clip_path  | The path the artist is clipped to                            |
| contains   | A picking function to test whether the artist contains the pick point |
| figure     | The figure instance the artist lives in, possibly None       |
| label      | A text label (e.g., for auto-labeling)                       |
| picker     | A python object that controls object picking                 |
| transform  | The transformation                                           |
| visible    | A boolean whether the artist should be drawn                 |
| zorder     | A number which determines the drawing order                  |
| rasterized | Boolean; Turns vectors into raster graphics (for compression & EPS transparency) |
