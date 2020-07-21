---
title: Novedades de las extensiones de lenguaje de SQL Server
titleSuffix: ''
description: Obtenga información sobre las novedades de las extensiones de lenguaje de SQL Server.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3bcf60c390b06695c4913bd1347045b807c1ae9d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "73658804"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>Novedades de las extensiones de lenguaje de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Se han agregado funcionalidades de [extensiones de lenguaje](language-extensions-overview.md) a SQL Server en cada versión a medida que se continúa la expansión, ampliación y profundización de la integración entre los lenguajes externos y la plataforma de datos. 

## <a name="new-in-sql-server-2019"></a>Novedades de SQL Server 2019 

Esta versión agrega compatibilidad con las extensiones de lenguaje de SQL Server. Para obtener más información sobre todas las características de esta versión, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) y [Notas de la versión de SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

- La instancia predeterminada de Java Runtime en Windows y Linux es Open Zulu JRE y se incluye con la instalación de [Extensiones de lenguaje de SQL Server en Windows](install/install-sql-server-language-extensions-on-windows.md) y la instalación de [Extensiones de lenguaje de SQL Server en Linux](../linux/sql-server-linux-setup-language-extensions.md).
- [Tipos de datos de Java](how-to/java-to-sql-data-types.md) admitidos.
- [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) para registrar un lenguaje externo (por ejemplo, Java) en SQL Server.
- [SDK de extensibilidad de Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md).
- En Windows y Linux, se puede acceder al código de Java en una biblioteca externa mediante la instrucción [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md). Más información: [Cómo llamar a Java desde SQL Server](how-to/call-java-from-sql.md).
- [Extensión del lenguaje Java](language-extensions-overview.md) en Windows y Linux. Puede poner código Java compilado a disposición de SQL Server asignando permisos y estableciendo la ruta de acceso. Las aplicaciones cliente con acceso a SQL Server pueden usar datos y ejecutar el código llamando a [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), el mismo procedimiento utilizado para la integración de R y Python en SQL Server Machine Learning Services.

## <a name="next-steps"></a>Pasos siguientes

+ Instalación de [extensiones de lenguaje de SQL Server en Windows](install/install-sql-server-language-extensions-on-windows.md) o [en Linux](../linux/sql-server-linux-setup-language-extensions.md)
