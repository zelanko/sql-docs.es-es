---
title: Restaurar una base de datos en el clúster de macrodatos de SQL Server | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 04514fb0184fa28e0ba959f3dd33cb2e1ec945cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796822"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>Restaurar una base de datos en la instancia maestra del clúster de SQL Server datos de gran tamaño

Para poner una base de datos de SQL Server existente en la instancia maestra, se recomienda usar una copia de seguridad, copia y restauración enfoque.  En este ejemplo se mostrará cómo restaurar la base de datos de AdventureWorks, pero puede utilizar cualquier copia de seguridad de base de datos que tiene.  Puede descargar la copia de seguridad de AdventureWorks [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=49502).

En primer lugar, la base de datos existente de SQL Server en SQL Server en Windows o Linux mediante cualquiera de los métodos habituales de la creación de una copia de seguridad de base de datos de copia de seguridad.

Copie el archivo de copia de seguridad en el contenedor de SQL Server en el pod de la instancia maestra del clúster de Kubernetes.

```bash
kubectl cp <path to .bak file> mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n <name of your cluster>
```

Ejemplo:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n clustertest
```

A continuación, compruebe que se copió el archivo de copia de seguridad en el contenedor de pod.

```bash
kubectl exec -it mssql-data-pool-master-0 -n <name of your cluster> -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
root@mssql-data-pool-master-0:/# exit
```

Ejemplo:

```bash
kubectl exec -it mssql-data-pool-master-0 -n clustertest -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
```

A continuación, restaure la copia de seguridad de base de datos a la instancia principal de SQL Server.  Si va a restaurar una copia de seguridad de base de datos que se creó en Windows, deberá obtener los nombres de los archivos.  En Studio Ops conectado a la instancia maestra, ejecute este script de SQL:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

Ejemplo:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![Lista de archivos de copia de seguridad](media/restore-database/database-restore-file-list.png)

Ahora, restaure la base de datos con un script similar al siguiente, sustituyendo los nombres o rutas de acceso según sea necesario según la copia de seguridad de base de datos.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

Ahora, si desea tener la base de datos de gran valor pueden tener acceso a los grupos de datos que necesita para configurar el grupo de datos de procedimientos almacenados, abra y ejecute estas secuencias de comandos desde el repositorio de GitHub.

Ejecute el **alto: valor de db-configuration\data_pool_ddl_install. SQL** secuencia de comandos.

- Los procedimientos almacenado de compatibilidad de configuración

Ejecute el **alto: valor de db-configuration\supportability. SQL** secuencia de comandos.
