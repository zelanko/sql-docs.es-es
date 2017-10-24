---
title: "Referencia de API de servicios de aprendizaje de máquina de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c776c43d66d01a2f721b5d3d8bc540741bf8b13
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="api-reference-for-sql-server-machine-learning-services"></a>Referencia de API de servicios de aprendizaje de máquina de SQL Server

Este artículo contiene vínculos a la documentación de referencia de API que se usan con SQL Server de aprendizaje automático. 

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

En su mayor parte, SQL Server utiliza las mismas bibliotecas de R y Python que se proporcionan en Microsoft R Server y servidor de aprendizaje de máquina de Microsoft. 

> [!NOTE]
> Documentación para todas las API se deriva de código fuente y no es posterior al editado.

## <a name="r"></a>L

+ [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

    Algoritmos escalables que admiten varios orígenes de datos y contextos de proceso remoto.

+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    Las transformaciones y los algoritmos de aprendizaje para R. requiere RevoScaleR máquina rápida y escalable.

+ [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr)

   Lee el esquema de orígenes de datos OLAP y ejecuta consultas MDX.

+ [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils)

    Funciones auxiliares para generar un procedimiento almacenado correcto desde el código de R.

+ [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)

   Funciones para establecer una sesión remota en una aplicación de consola y para publicar y administrar un servicio web que usa código de R o Python.

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

    Equivalente de Python del paquete RevoScaleR para el lenguaje R. Es compatible con los mismos orígenes de datos y contextos de proceso.

+ [Microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

    Equivalente de Python de la MicrosoftML del paquete de R. es compatible con los mismos contextos de proceso y orígenes de datos e incluye rápido, algoritmos escalables y transformaciones de Microsoft.

## <a name="related-apis"></a>API relacionadas

+ [Referencia a la función RevoPEMAR](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

    Admite el desarrollo de algoritmos paralelos

+ [RevoUtils](https://docs.microsoft.com/r-server/r-reference/revoutils/revoutils)

    Funciones de utilidad para su uso con entornos de RevoScaleR

## <a name="other"></a>Otro

Temas "Cómo" y resúmenes específicas para el uso de estas R o las API de Python en SQL Server pueden encontrarse aquí:

+ [Funciones scaleR para trabajar con SQL Server](scaler-functions-for-working-with-sql-server-data.md)
+ [Generar un procedimiento almacenado mediante sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [Leer datos de MDX en R mediante olapR](how-to-create-mdx-queries-using-olapr.md)

