![Python Import System](./Python_Import_System.svg)

Diagram is drawn based on python's [office documentation][1]

## Pseudo code

```python
# import name, __import__(name), importlib.import_module(name), etc

if name in sys.modules:
    if sys.modules[name] is None:
        raise ModuleNotFoundError
    else if "from import statement":
        locals()[name] = module
    else:
        return module
else:
    for finder in sys.meta_path:
        spec = finder.find_spec(name, ...)
        if spec is not None:
            if spec.loader is None:
                raise ImportError
            else:
                module = spec.loader.create_module(spec)
                spec.loader.exec_module(module)
                if "from import statement":
                    locals()[name] = module
                else:
                    return module
        else:
            continue
    else:
        raise ModuleNotFoundError
```

## Experiments

See [playground.ipynb](./playground.ipynb) for some experiments on the diagram.

[1]: https://docs.python.org/3/reference/import.html

