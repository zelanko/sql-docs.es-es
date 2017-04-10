---
title: "Supervisar R Services con informes personalizados en Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "02/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Supervisar R Services con informes personalizados en Management Studio
Para facilitar la administración de SQL Server R Services, el equipo del producto ha ofrecido una serie de informes personalizados de ejemplo que se pueden agregar a SQL Server Management Studio para ver los detalles de R Services del siguiente modo:

- Lista de las sesiones activas de R
- Configuración R de la instancia actual
- Estadísticas de ejecución para el tiempo de ejecución de R
- Lista de eventos extendidos de R Services
- Lista de paquetes de R instalados en la instancia actual

En este tema se explica cómo instalar y usar los informes. Para obtener más información sobre los informes personalizados en Management Studio, consulte [Informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Cómo instalar los informes

Los informes se diseñan mediante SQL Server Reporting Services, pero pueden utilizarse directamente desde SQL Server Management Studio, incluso aunque Reporting Services no esté instalado en la instancia. 

Para utilizar estos informes:

* Descargue los archivos RDL desde el repositorio de GitHub para obtener ejemplos de productos de SQL Server.
* Agregue los archivos a la carpeta de informes personalizados utilizada por SQL Server Management Studio.
* Abra los informes en SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Paso 1. Descargar los informes

1. Abra el repositorio de GitHub que contiene ejemplos de todos los productos de SQL Server, incluidas las bases de datos de ejemplo. 
   + [Microsoft/sql-server-samples](https://github.com/Microsoft/sql-server-samples)
   + [Informes personalizados de SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/SSMS-Custom-Reports)
      
2. Para descargar los ejemplos, también puede iniciar sesión en GitHub y realizar una bifurcación local de los ejemplos. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>Paso 2. Copiar los informes en Management Studio

3. Ubique la carpeta de informes personalizados utilizada por SQL Server Management Studio. De forma predeterminada, los informes personalizados se almacenan en esta carpeta:
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   Sin embargo, puede especificar una carpeta diferente o crear subcarpetas.

4. Copie los archivos *.RDL en la carpeta de informes personalizados.


### <a name="step-3-run-the-reports"></a>Paso 3. Ejecutar los informes

5. En Management Studio, haga clic en el nodo **Bases de datos** de la instancia donde quiere ejecutar los informes.
6. Haga clic en **Informes** y, después, en **Informes personalizados**. 
7. En el cuadro de diálogo **Abrir archivo**, ubique la carpeta de informes personalizados.
8. Seleccione uno de los archivos RDL que descargó y, luego, haga clic en **Abrir**.

> [!IMPORTANT] En algunos equipos, como los dispositivos con pantallas con valores altos de PPP o una resolución superior a 1080p, en algunas sesiones de escritorio remoto, no se pueden utilizar estos informes. Hay un error en el control de visor de informes en SSMS que se bloquea el informe.  


## <a name="report-list"></a>Lista de informes

Actualmente, el repositorio de ejemplos de productos en GitHub incluye los siguientes informes para SQL Server R Services:

+ **R Services: sesiones activas**

  Utilice este informe para ver los usuarios que están conectados actualmente a la instancia de SQL y que ejecutan trabajos de R. 
  
+ **R Services: configuración**

  Utilice este informe para ver las propiedades del tiempo de ejecución de R y de la configuración de R Services. El informe indicará si es necesario un reinicio y buscará los protocolos de red necesarios. 
  
  Se necesita la autenticación implícita para ejecutar R en un contexto de proceso SQL, para ello, el informe comprueba si existe un inicio de sesión de base de datos para el grupo SQLRUserGroup.

  > [!NOTE] Para obtener más información sobre estos campos, consulte [Package metadata](http://r-pkgs.had.co.nz/description.html) (Metadatos de paquetes) de Hadley Wickham. Por ejemplo,se introdujo el campo *Alias* para el tiempo de ejecución de R con el fin de ayudar a diferenciar entre versiones. 

 + **R Services : configuración de una instancia** 

   Este informe está pensado para ayudarle a configurar R Services después de la instalación. Puede ejecutarlo desde el informe anterior si R Services no está configurado correctamente.
 
+ **R Services: estadísticas de ejecución**

  Utilice este informe para ver las estadísticas de ejecución de R Services. Por ejemplo, puede obtener el número total de secuencias de comandos de R que se han ejecutado, el número de ejecuciones en paralelo y las funciones RevoScaleR utilizadas con más frecuencia.
  Actualmente el informe solo supervisa estadísticas para las funciones del paquete de RevoScaleR.
  Haga clic en **Ver script de SQL** para obtener el código de T-SQL de este informe. 

+ **R Services: eventos extendidos**

  Utilice este informe para ver una lista de los eventos extendidos que están disponibles para supervisar la ejecución de la secuencia de comandos de R. 
  Haga clic en **Ver script de SQL** para obtener el código de T-SQL de este informe.

+ **R Services: paquetes**

  Utilice este informe para ver una lista de los paquetes de R instalados en la instancia de SQL Server. El informe incluye actualmente estas propiedades de paquete: 
  + Paquete (nombre)
  + Versión 
  + Depende
  + Licencia
  + Creado
  + Ruta de acceso lib

+ **R Services: uso de recursos**

  Utilice este informe para ver el consumo de recursos de CPU, memoria y recursos de E/S por parte de la ejecución de secuencias de comandos de SQL Server R. También puede ver la configuración de la memoria de grupos de recursos externos. 


## <a name="see-also"></a>Vea también

[Supervisar R Services](../../advanced-analytics/r-services/monitoring-r-services.md)

[Eventos extendidos para R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)