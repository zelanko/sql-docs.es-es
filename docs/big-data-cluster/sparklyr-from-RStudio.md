---
title: Usar sparklyr de RStudio
titleSuffix: SQL Server big data clusters
description: Conéctese al clúster de macrodatos con sparklyr de RStudio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8004146499bd8b17c7705f7558de075dfece5813
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994177"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>Usar sparklyr en clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr proporciona una interfaz de R para Apache Spark. Sparklyr es una forma popular para los desarrolladores de R usen Spark. Este artículo describe cómo usar sparklyr en un clúster de macrodatos de 2019 de SQL Server (versión preliminar) mediante RStudio.

## <a name="prerequisites"></a>Requisitos previos

- [Implementar un clúster de SQL Server 2019 macrodatos](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>Instalar RStudio Desktop

Instalar y configurar **RStudio Desktop** con los pasos siguientes:

1. Si está ejecutando en un cliente de Windows, [descargar e instalar R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [Descargar e instalar RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

1. Una vez finalizada la instalación, ejecute los siguientes comandos dentro de RStudio Desktop para instalar los paquetes necesarios:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>Conexión a Spark en un clúster de macrodatos

Puede usar sparklyr para conectarse desde un cliente para el clúster de macrodatos con Livy y la puerta de enlace de Spark o HDFS. 

En RStudio, cree un script de R y conectarse a Spark en el ejemplo siguiente:

> [!TIP]
> Para el `<USERNAME>` y `<PASSWORD>` valores, use el nombre de usuario (como raíz) y la contraseña que estableció durante la implementación del clúster de macrodatos. Para el `<IP>` y `<PORT>` valores, consulte la documentación sobre [conectarse a un clúster de macrodatos](connect-to-big-data-cluster.md).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Ejecutar consultas de sparklyr

Después de conectarse a Spark, puede ejecutar sparklyr. El ejemplo siguiente realiza una consulta en el conjunto de datos de iris mediante sparklyr:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>Cálculos de R distribuidos

Una característica de sparklyr es la capacidad de [distribuyen los cálculos de R](https://spark.rstudio.com/guides/distributed-r/) con [spark_apply](https://spark.rstudio.com/reference/spark_apply/).

Dado que los clústeres de datos de gran tamaño usan conexiones de Livy, debe establecer `packages = FALSE` en la llamada a **spark_apply**. Para obtener más información, consulte el [sección Livy](https://spark.rstudio.com/guides/distributed-r/#livy) de la documentación de sparklyr en cálculos R distribuidos. Con esta configuración, solo puede usar los paquetes de R que ya están instalados en el clúster de Spark en el código de R que se pasa a **spark_apply**. El ejemplo siguiente muestra esta funcionalidad:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos](big-data-cluster-overview.md).
