# ENV variable

- `os.environ["PATH"]`
  - throw exception if key doesn't exist
- `os.environ.get('PATH')`
  - return None if missing
- `os.environ.get('PATH', "DEFAULT")`
  - return default if missing
- `os.environ['PATH']="something`
  - mutate variable
