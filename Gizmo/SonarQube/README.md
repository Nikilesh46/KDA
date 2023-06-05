
#### SonarQube ####

SonarQube is a self-managed, automatic code review tool that systematically helps you deliver clean code. As a core element of our Sonar solution, SonarQube integrates into your existing workflow and detects issues in your code to help you perform continuous code inspections of your projects. The tool analyses 30+ different programming languages and integrates into your CI pipeline and DevOps platform to ensure that your code meets high-quality standards.

#####Installation #####

The SonarQube server running the following processes:
A web server that serves the SonarQube user interface.
A search server based on Elasticsearch.
The compute engine in charge of processing code analysis reports and saving them in the SonarQube database.
The database to store the following:
Metrics and issues for code quality and security generated during code scans.
The SonarQube instance configuration.
One or more scanners running on your build or continuous integration servers to analyze projects.


Several external database engines are supported. Be sure to follow the requirements listed for your database. They are real requirements not recommendations.
  MS SQL Server
  Oracle
  PostgreSQL

The SonarQube server can be installed directly, through Docker or through Docker Compose 
