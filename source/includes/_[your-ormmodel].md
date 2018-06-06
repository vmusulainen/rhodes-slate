# Rho.[Your-OrmModel]

All methods here are accessed from the model instance object that you have created. In places where you see `[Your-OrmModel]` on this page, you would use the instance object instead.

    :::js
    var productModel = Rho.ORM.addModel(function(model){
      model.modelName("Product");
      model.enable("sync");
      model.property("name","string");
      model.property("brand","string");
      model.property("price","float");
      model.set("partition","user");
    });

    // create model object and save it to database
    var product = productModel.create({
      brand: 'Apple',
      name: 'iPhone5',
      price: 199.99});

    // read product from database
    var product = productModel.find('first');
    product.get('brand'); // Apple
    product.get('name'); // iPhone5

        