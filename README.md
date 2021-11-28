# MODIS_LAI
var dataset = ee.Image('MODIS/006/MCD15A3H/2021_08_01').select('Lai').clip(senegal);
// var defaultVisualization = dataset.first().select('Lai');
var defaultVisualizationVis = {
  min: 0.0,
  max: 8.0,
  palette: ['e1e4b4', '999d60', '2ec409', '0a4b06'],
};
Map.setCenter(-15.10, 14.69, 7);
Map.addLayer(
    dataset.clip(senegal), defaultVisualizationVis, 'Default visualization');



////my LEGEND/////////////////////////////

var panel = ui.Panel({
  style: {
    position: 'top-left',
    padding: '5px;'
  }
})

var title = ui.Label({
  value: 'LAI',
  style: {
    fontSize: '24px',
    fontWeight: 'bold',
    margin: '10px;'
  }
})

panel.add(title)

var color = ['e1e4b4','999d60','2ec409','0a4b06']
var lc_class = ['solnu', 'tapi herbace', 'vegetation moyen dense', 'vegetation tres dense']

var list_legend = function(color, description) {
  
  var c = ui.Label({
    style: {
      backgroundColor: color,
      padding: '10px',
      margin: '4px'
    }
  })
  
  var ds = ui.Label({
    value: description,
    style: {
      margin: '5px'
    }
  })
  
  return ui.Panel({
    widgets: [c, ds],
    layout: ui.Panel.Layout.Flow('horizontal')
  })
}

for(var a = 0; a < 4; a++){
  panel.add(list_legend(color[a], lc_class[a]))
}

Map.add(panel)
/////////time series////////////////////////////////////////////////



