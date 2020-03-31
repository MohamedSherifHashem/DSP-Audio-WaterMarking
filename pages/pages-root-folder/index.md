---
#
# Use the widgets beneath and the content will be
# inserted automagically in the webpage. To make
# this work, you have to use › layout: frontpage
#
layout: frontpage
header:
 image_fullwidth: logo.jpg
widget1:
  title: "Design"
  url: 'https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/design/'
  image: widget-1-302x182.jpg
  text: 'check out our design'
widget2: widget-2-302x182.jpg
  title: "How to use it ?"
  url: 'https://mohamedsherifhashem.github.io/DSP-Audio-WaterMarking/getting-started/'
  text: 'Start watermarking your audio now ...'
widget3:widget-3-302x182.jpg
  title: "Related Work"
  url: 'https://mohamedsherifhashem.github.io/DSP-Audio-WaterMarking/reports/relatedwork/'
  text: 'Check out what other techniques people use'
#
# Use the call for action to show a button on the frontpage
#
# To make internal links, just use a permalink like this
# url: /getting-started/
#
# To style the button in different colors, use no value
# to use the main color or success, alert or secondary.
# To change colors see sass/_01_settings_colors.scss
#
callforaction:
  url: https://mohamedsherifhashem.github.io/DSP-Audio-WaterMarking/roadmap/
  text: Check new features  ›
  style: alert
permalink: /index.html
#
# This is a nasty hack to make the navigation highlight
# this page as active in the topbar navigation
#
homepage: true
---
