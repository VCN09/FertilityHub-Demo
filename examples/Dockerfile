FROM python:3.10-slimWORKDIR /appCOPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txtCOPY . .CMD ["gunicorn", "--bind", "0.0.0.0:5000", "wsgi:app"]
