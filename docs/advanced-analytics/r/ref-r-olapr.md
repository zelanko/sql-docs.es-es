---
title: Biblioteca de funciones de R de OLAP
description: Introducción a la biblioteca de funciones de olapr en SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 674e4ed4d1967452093e81e7bb4f5518d9237cf6
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469976"
---
# <a name="olapr-r-library-in-sql-server"></a>olapr (biblioteca de R en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapr** es una biblioteca de Microsoft de funciones de R que se usa para las consultas MDX en un cubo OLAP SQL Server Analysis Services. Las funciones no admiten todas las operaciones MDX, pero puede crear consultas que recorten, los índices, la obtención de detalles, el Resumen y los pivotes en las dimensiones. 

Este paquete no se ha cargado previamente en una sesión de R. Ejecute el siguiente comando para cargar la biblioteca.

```R
library(olapR)
```

Puede usar esta biblioteca en las conexiones a un Analysis Services cubo OLAP en todas las versiones compatibles de SQL Server. En este momento no se admiten las conexiones a un modelo tabular.

## <a name="package-version"></a>Versión del paquete

La versión actual es 1.0.0 en todos los productos solo de Windows y descargas que proporcionan la biblioteca.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

La  biblioteca de olapr se distribuye en varios productos de Microsoft, pero el uso es el mismo si se obtiene la biblioteca en SQL Server u otro producto. Dado que las funciones son iguales, la [documentación de las funciones individuales de sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft machine learning Server. Si hay algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="availability-and-location"></a>Disponibilidad y ubicación

Este paquete se proporciona en los siguientes productos, así como en varias imágenes de máquina virtual en Azure. La ubicación del paquete varía en consecuencia.

Producto | Location |
--------|----------|
SQL Server 2017 Machine Learning Services (con la integración de R) | C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Archivos de Programa\microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Archivos de Files\Microsoft\R_SERVER\library |
Cliente de Microsoft R | C:\Archivos de Files\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (en Azure) | C:\Archivos de Files\Microsoft\R Client\R_SERVER\library |
SQL Server máquina virtual (en Azure) <sup>1</sup> | C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> la integración de R es opcional en SQL Server. La biblioteca de olapr se instalará cuando agregue la característica Machine Learning o R durante la configuración de la máquina virtual.


## <a name="see-also"></a>Vea también

[Cómo crear consultas MDX con olapr](how-to-create-mdx-queries-using-olapr.md)
