# REPORT API

This application deals with some common operation for Suade Reports. In particular, it allows to
- List the available *reports*
- Get XML representation of specific *report*
- Get PDF representation of specific *report*

The application is a Flask application composed by three main components:
- the *model* containing the representation of the *Report* along with the methods for the model conversion into json and xml.
- the *store* containing the sql alchemy representation of the *Report* along with the methods for retrieving the data from the database
- the *route* containing the *endpoints*
- the *templates* containing a HTML template of support to produce the PDF representation

Please note that for a design choice if the reports stored into the database contains not json compliant data the *ListReports* endpoint will raise a 500 error.

## Installation

The required libraries are listed into the requirements.txt, so that you can install them by means of the following command:
`pip install -r requirements.txt`.

Please note that for the generation of the PDF the **WeasyPrint** library is used. To install it refers to [WeasyPrint](http://weasyprint.readthedocs.io/en/latest/install.html).

## Usage

The application is flask application and in order to connect to the database requires to set both the **DB_USER** and **DB_PASSWORD** variables. The server will listen by default on the 8080 port but it is possible to customise it setting the **SERVER_PORT** environment variable. 

After setting the environment variables listed above, to run the system go into the  by means of the following command:
`python report-app.py`

Once that the server is running it's possible to send GET requests to the following endpoints:
- **/api/reports** to list the available reports. The returned reports are in the JSON format.
- **/api/reports/<int:report_id>.xml** to get the XML representation of the report identified by the *report_id*.
- **/api/reports/<int:report_id>.pdf** to get the PDF representation of the report identified by the *report_id*.

## API Documentation

To document the API *Swagger* and *flasgger* are used. The *yml* file are stored under the *doc* folder. Once the server is run it's possible to see the API Documentation through [http://127.0.0.1:8080/apidocs/](http://127.0.0.1:8080/apidocs/). Remember that if you set the **SERVER_PORT** env variable also the documentation will be available at that port.

## Testing

To test the system it's possible to run from the *tests* module the following command:
`nosetests -v --with-coverage --cover-package=app .`

