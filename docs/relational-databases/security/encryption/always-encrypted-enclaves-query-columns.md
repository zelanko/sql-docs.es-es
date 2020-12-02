---
description: Consulta de columnas mediante Always Encrypted con enclaves seguros
title: Consulta de columnas mediante Always Encrypted con enclaves seguros | Microsoft Docs
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
ms.openlocfilehash: 8daabf320e0f736bcfabc5addb8508320b10bb8f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88482228"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Consulta de columnas mediante Always Encrypted con enclaves seguros
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

En este artículo se reúnen las consideraciones generales para ejecutar consultas en columnas cifradas usando un enclave seguro de servidor para [Always Encrypted con enclaves seguros](always-encrypted-enclaves.md). 

Los siguientes tipos de consulta conllevan el uso de un enclave seguro:
- Consultas que desencadenan operaciones criptográficas en contexto mediante claves habilitadas para el enclave; vea [Configuración del cifrado de columnas en contexto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md).
- *Consultas enriquecidas*: comparaciones de intervalo u operaciones de coincidencia de patrones en columnas cifradas que usan cifrado aleatorio y claves habilitadas para el enclave.
- Consultas que crean o actualizan índices en columnas cifradas que usan cifrado aleatorio y claves habilitadas para el enclave. Para más información, vea [Creación y uso de índices en columnas de Always Encrypted con enclaves seguros](always-encrypted-enclaves-create-use-indexes.md).

> [!NOTE]
> Las consultas y los índices enriquecidos solo se admiten en columnas habilitadas para el enclave (columnas cifradas con claves de cifrado de columnas habilitadas para el enclave) que usen cifrado aleatorio. El cifrado determinista no admite ni consultas ni índices enriquecidos.

> [!NOTE]
> Las consultas enriquecidas relativas a columnas de cadena de caracteres cifradas requieren que las columnas usen intercalaciones con un criterio de ordenación binary2 (intercalaciones BIN2). 


## <a name="next-steps"></a>Pasos siguientes
- [Consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="see-also"></a>Consulte también
- [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)

