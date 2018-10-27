### <a id="sampledata"></a> Cargar datos de ejemplo

Tutoriales de clúster de macrodatos de SQL Server usan un conjunto común de datos de ejemplo. Use los pasos siguientes para configurar los datos de ejemplo en el clúster de macrodatos:

1. Si no tiene las herramientas de línea de comandos de SQL Server (**sqlcmd** y **bcp**) instalado, instalar estas herramientas con uno de los vínculos:

   * **Windows**: [herramientas de línea de comandos de instalación de SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=53591)
   * **Linux**: [herramientas de línea de comandos de instalación de SQL Server en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-tools)

1. Descargue el archivo de copia de seguridad de ejemplo [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) en el equipo.

1. Vaya al clúster de macrodatos de SQL Server 2019 [directorio samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster).

1. Descargue el [bootstrap-ejemplo-db.sql](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql) script Transact-SQL.

1. Descargue y ejecute uno de los siguientes scripts de dos desde la línea de comandos:

   * **Windows**: [bootstrap-ejemplo-db.cmd](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd)
   * **Linux**: [bootstrap-ejemplo-db.sh](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh)

   > [!TIP]
   > Puede obtener las instrucciones de uso mediante la ejecución de la secuencia de comandos sin parámetros.

El script restaura la base de datos de ejemplo en la instancia principal de SQL Server y también carga datos en HDFS en el bloque de almacenamiento.