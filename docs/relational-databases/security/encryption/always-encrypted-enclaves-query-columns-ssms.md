---
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
ms.openlocfilehash: 6bee04f4a794a503b89b73d4ef4a6a1cef897b4b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595600"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>Consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

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

