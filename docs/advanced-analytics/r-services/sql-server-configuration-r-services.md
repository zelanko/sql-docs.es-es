---
title: "Configuraci&#243;n de SQL Server (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Configuraci&#243;n de SQL Server (R Services)
La información de esta sección proporciona instrucciones generales sobre la configuración de hardware y de red del equipo que se utiliza para hospedar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Debe considerarse además general [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] performance tuning de la información proporcionada en el [Centro de rendimiento para el motor de base de datos de SQL Server y base de datos de SQL Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## Procesador

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] puede realizar tareas en paralelo con los núcleos disponibles en el equipo; núcleos que están disponibles, mejor será el rendimiento. Puesto que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] suele ser utilizado por varios usuarios simultáneamente, el Administrador de la base de datos debe determinar el número ideal de núcleos que se necesitan para admitir cálculos de máxima carga de trabajo. Aunque no sea de ayuda el número de núcleos para operaciones enlazado a E/S, de la CPU algoritmos se beneficiarán de CPU más rápidas con varios núcleos.

## Memoria

La cantidad de memoria disponible en el equipo puede tener un gran impacto en el rendimiento de los algoritmos de análisis avanzados. Memoria insuficiente puede afectar el grado de paralelismo cuando se usa el contexto del proceso SQL. También puede afectar el tamaño del fragmento (filas por operación de lectura) que se puede procesar y el número de sesiones simultáneas que se admiten.

Se recomienda un mínimo de 32GB. Si tiene más de 32GB disponible, puede configurar el origen de datos SQL para utilizar más filas en cada operación de lectura para mejorar el rendimiento.

## Opciones de energía

En el sistema operativo Windows, la __de alto rendimiento__ debe utilizarse la opción de energía. Mediante la configuración de energía diferente, provocará incoherente o una disminución de rendimiento al usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

## E/S de disco

Trabajos de entrenamiento y la predicción mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] son inherentemente IO enlazado y dependen de la velocidad de los discos que se almacena la base de datos en. Unidades de disco más rápidas, como unidades de estado sólido (SSD) pueden ayudar. 

E/S de disco también se ve afectado por otras aplicaciones de acceso al disco: por ejemplo, leer las operaciones en una base de datos de otros clientes. Rendimiento de E/S de disco también puede ser afectado por la configuración del sistema de archivos en uso, como el tamaño de bloque utilizado por el sistema de archivos. Si hay varias unidades, almacenar las bases de datos en una unidad distinta de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] hasta que las solicitudes de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no alcanza el mismo disco como solicitudes para datos almacenados en la base de datos.

E/S de disco también enormemente pueden afectar al rendimiento cuando se ejecuta RevoScaleR funciones analíticas que utilizan varias iteraciones durante el entrenamiento. Por ejemplo, `rxLogit`, `rxDTree`, `rxDForest` y `rxBTrees` utilizan varias iteraciones. Cuando el origen de datos es [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], estos algoritmos utilizan archivos temporales que se optimizan para capturar los datos. Estos archivos se limpian automáticamente una vez finalizada la sesión. Tener un disco de alto rendimiento para las operaciones de lectura y escritura puede mejorar significativamente el tiempo global transcurrido para estos algoritmos.

> [!NOTE]
> [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] requiere soporte de nombre de archivo 8.3 en sistemas operativos Windows. Puede utilizar fsutil.exe para determinar si una unidad admite nombres de 8.3 archivo o para habilitar la compatibilidad si no es así. Para obtener más información sobre el uso de fsutil.exe con nombres de 8.3 archivo, consulte [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

### Compresión de tabla

A menudo puede mejorarse el rendimiento de E/S mediante compresión o columstore índices. Por lo general, datos a menudo se repiten en varias columnas en una tabla, por lo que el uso de un índice de almacén aprovecha estas repeticiones al comprimir los datos.

Un índice de almacén podría no ser tan eficaz si hay una gran cantidad de inserciones en la tabla, pero es una buena opción si los datos son estáticos o sólo cambian con poca frecuencia. Si un almacén de columnas no es adecuado, al habilitar la compresión en una tabla principal de la fila puede utilizarse para mejorar la optimización de INFRAESTRUCTURA.

Para obtener más información, consulte los siguientes documentos:

* [Comprimir datos](../../relational-databases/data-compression/data-compression.md)

* [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Guía de índices de almacén de columnas](Columnstore%20Indexes%20Guide.md)

## Archivo de paginación

El sistema operativo Windows usa un archivo de paginación para administrar los volcados de memoria y para almacenar páginas de memoria virtual. Si observa una paginación excesiva, considere la posibilidad de aumentar la memoria física en el equipo. Aunque tener más memoria física no elimina la paginación, reduce la necesidad de paginación.

La velocidad del disco que se almacena el archivo de paginación en también puede afectar al rendimiento. Almacenar el archivo de paginación en un SSD o usar varios archivos de página entre varios SSD, puede mejorar el rendimiento.

Vea [cómo determinar el tamaño del archivo de página adecuado para versiones de 64 bits de Windows](https://support.microsoft.com/en-us/kb/2860880) para obtener información sobre el archivo de paginación de tamaño.

## Gobierno de recursos

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] admite el regulador de recursos para controlar los distintos recursos que usa [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Por ejemplo, se limita a 20% de la memoria total disponible para el valor predeterminado para su consumo de memoria por R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Esto se hace para asegurarse de que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] flujos de trabajo no se ve muy afectados por los trabajos de larga ejecución R. Sin embargo, el Administrador de la base de datos pueden cambiar estos límites. 

Los recursos limitados __MAX_CPU_PERCENT__, __MAX_MEMORY_PERCENT__, y __MAX_PROCESSES__. Para ver la configuración actual, utilice este [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instrucción:

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

Si [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] es, principalmente, se utiliza para los servicios de R, puede resultar útil aumentar MAX_CPU_PERCENT hasta un 40% y el 60%. Si hay muchas sesiones de R con el mismo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] al mismo tiempo, se incrementará los tres. Para cambiar los valores de los recursos asignados, use [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instrucciones. 

Este ejemplo establece el uso de memoria en un 40%:

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
El ejemplo siguiente establece los tres valores configurables:
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> Para realizar cambios en estos valores surten efecto inmediatamente, ejecute la instrucción `ALTER RESOURCE GOVERNOR RECONFIGURE` después de cambiar una configuración de proceso máximo, CPU o memoria. 

## Vea también
[Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

[CREAR GRUPO DE RECURSOS EXTERNOS](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [Guía de optimización de rendimiento de SQL Server R servicios](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [Caso práctico de rendimiento](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R y optimización de datos](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)