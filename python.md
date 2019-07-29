
# python notes

## exception with notes

```python
except Exception as e:
	trace_back = sys.exc_info()[2]
	line = trace_back.tb_lineno
	raise FlowException("Process Exception in line {}".format(line), e)
```
