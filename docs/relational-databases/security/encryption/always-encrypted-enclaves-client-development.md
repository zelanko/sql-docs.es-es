---
title: Desarrollo de aplicaciones mediante Always Encrypted con enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 54e282e7d68c23837c1865f1257ba7e159644d26
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595540"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desarrollo de aplicaciones mediante Always Encrypted con enclaves seguros
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[Always Encrypted con enclaves seguros](always-encrypted-enclaves.md) amplía [Always Encrypted](always-encrypted-database-engine.md) para habilitar funcionalidades más completas de las consultas de la aplicación en columnas de bases de datos confidenciales cifradas. Aprovecha las tecnologías de enclaves seguros para permitir que el ejecutor de las consultas en [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] delegue los cálculos de las columnas cifradas en un enclave seguro dentro del proceso de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

## <a name="client-driver-for-always-encrypted-with-secure-enclaves"></a>Controlador de cliente para Always Encrypted con enclaves seguros

Para desarrollar aplicaciones mediante Always Encrypted con enclaves seguros, necesita una versión del controlador de cliente de SQL que admita los enclaves seguros. El controlador de cliente desempeña un papel fundamental:
- Antes de enviar una consulta que usa un enclave seguro a [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para su ejecución, el controlador inicia la atestación del enclave para comprobar que el enclave seguro es de confianza y que se puede usar de forma segura para procesar datos confidenciales. Para obtener más información sobre la atestación, consulte [Atestación de un enclave seguro](always-encrypted-enclaves.md#secure-enclave-attestation).
- Una vez que la atestación se ha realizado correctamente, el controlador de cliente negocia un secreto compartido para establecer una sesión segura con el enclave.
- El controlador usa el secreto compartido para cifrar las claves de cifrado de columna que el enclave necesitará para procesar la consulta y envía las claves a [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], que las reenvía al enclave seguro que descifra las claves. 
- Por último, el controlador envía la consulta para su ejecución, lo que desencadena los cálculos dentro del enclave seguro.

Para usar la funcionalidad del enclave seguro, debe configurar la aplicación y el controlador cliente a fin de habilitar los cálculos del enclave cuando se conecta a la base de datos y especifica un punto de conexión del servicio de atestación (una dirección URL de atestación de enclave) que apunte a un servicio de atestación para el enclave. Los detalles dependen del controlador y del servicio o protocolo de atestación que use.

## <a name="next-steps"></a>Pasos siguientes

Los siguientes controladores de cliente admiten Always Encrypted con enclaves seguros:
- Proveedor de datos .NET Framework para SQL Server en .NET Framework 4.7.2 o superior. 
    - Para obtener más información, consulte [Uso de Always Encrypted con el proveedor de datos .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md).
    - Para ver un tutorial paso a paso, consulte [Tutorial: Desarrollo de una aplicación de .NET Framework mediante Always Encrypted con enclaves seguros](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md).
- Microsoft ODBC Driver for SQL Server, versión 17.4 o superior. 
    - Para obtener más información, vea [Uso de Always Encrypted con ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md). 
    - Para obtener información sobre cómo habilitar los cálculos del enclave para una conexión de base de datos mediante ODBC, consulte la sección [Habilitación de Always Encrypted con enclaves seguros](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves).
