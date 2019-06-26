This is [ChakraCore](https://github.com/microsoft/ChakraCore) implementation for Delphi.

For successful usage you should take [tondrej](https://github.com/tondrej) bindings and classes from [here](https://github.com/tondrej/chakracore-delphi).

This implementation is very simple without any native callback from JavaScript etc.

Full example of usage:
```delphi
var
  engine: TChakraCoreEngine;
begin
  engine := TChakraCoreEngine.Create();
  
  engine.SetNewObject('obj'); // set a new object
  engine.SetNewObject('obj2.a'); // or set a new object with new object inside
  engine.SetVarBoolean('obj.b', True); // set a bool value inside object
  engine.SetVarInteger('obj.i', 1); // set an int value inside object
  engine.SetVarLong('obj.l', 1000000000000); // set a long value inside object
  engine.SetVarNull('obj.n'); // set a null value inside object
  engine.SetVarString('obj.s', 'new string'); // set a string value inside object
  engine.SetVarFromEvaluate('obj2.newThis', 'this;'); // set a value from evaluate
  engine.SetVarFromScript('obj2.intRef', 'obj.i'); // set a value from existing variable

  engine.Script.Append('var r = obj2.intRef + obj.l;'); // add code to the Script
  engine.Execute(); // and execute
  
  engine.Execute('var r = obj2.intRef + obj.l;'); // or execute code instantly

  Writeln(engine.GetVarAsString('r')); // get a variable as string (calling `toString()`)
  Writeln(engine.GetVarAsString('obj.l'));
  Writeln(engine.GetVarFromEvaluate('obj.i + obj.i;')); // execute and get result as string

  engine.Destroy();
end;
```
