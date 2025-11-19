###Inserción de documento nuevo###
db.estudiante.insertOne({
  Symbol: "TEST", 
  Name: "TEST COMPANY",
  Sector: "TESTER",
  Price: 175.43,
})

###Selección de Sector específico###
db.estudiante.find({ Sector: "Advertising" })

###Actualización de datos###
db.estudiante.updateOne(
  { Symbol: "TEST" },
  { $set: { Name: "Cambio de Nombre" } }
)

###Eliminación###
db.estudiante.deleteOne({ Symbol: "TEST" }) 

###Precio mayor que 300###
db.estudiante.find({ Price: { $gt: 300 } })

###Compañías con PER < 20###
db.estudiante.find({
  'Price/Earnings': { $lt: 20 }
})

###Rango de precios 50–100###
db.estudiante.find({
  Price: { $gte: 50, $lte: 100 }
})

###Contar empresas por Sector###
db.estudiante.aggregate([
  { $group: { _id: "$Sector", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
])

###Promedio del precio por Sector###
db.estudiante.aggregate([
  { $group: { _id: "$Sector", avg_Price: { $avg: "$Price" } } },
  { $sort: { avg_Price: -1 } }
])

###Top 10 por Market Cap###
db.estudiante.aggregate([
  { $sort: { Market_cap: -1 } },
  { $limit: 10 }
])

###Top 10 dividend yield###
db.estudiante.aggregate([
  { $sort: { dividend_yield: -1 } },
  { $limit: 10 }
])
