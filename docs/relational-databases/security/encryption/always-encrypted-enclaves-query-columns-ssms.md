---
description: Consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS
title: Consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 74149cdcf8dd12280103c592c5a8662dddf4e750
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470097"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>Consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

En este artículo se describe cómo usar SQL Server Management Studio para emitir consultas que usan un enclave seguro del lado servidor para [Always Encrypted con enclaves seguros](always-encrypted-enclaves.md), incluido lo siguiente:
- Consultas que desencadenan operaciones criptográficas en contexto.
- Consultas que desencadenan cálculos completos, incluidas comparaciones de intervalo u operaciones de coincidencia de patrones en columnas cifradas con claves habilitadas para el enclave.
- Consultas que crean o actualizan índices en columnas cifradas que usan cifrado aleatorio y claves habilitadas para el enclave.  

Para usar SSMS para ejecutar consultas en columnas cifradas mediante un enclave seguro, siga las instrucciones indicadas en [Consulta de columnas mediante Always Encrypted con SQL Server Management Studio](always-encrypted-query-columns-ssms.md). A continuación se indican algunos aspectos específicos de los enclaves que debe tener en cuenta:

- Necesita la versión 18.3 o posterior de SSMS.
- Asegúrese de ejecutar las consultas en una ventana de consulta que use un enclave seguro de una conexión con Always Encrypted y los cálculos de enclave habilitados. Para obtener instrucciones detalladas, consulte [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md) y [Habilitación y deshabilitación de Always Encrypted para una conexión de base de datos](always-encrypted-query-columns-ssms.md#en-dis).

## <a name="next-steps"></a>Pasos siguientes
- [Desarrollo de aplicaciones mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>Consulte también  
- [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Configuración del cifrado de columnas en contexto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Creación y uso de índices en columnas mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)

