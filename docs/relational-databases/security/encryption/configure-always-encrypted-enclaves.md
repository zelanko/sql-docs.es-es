---
title: Configuración y uso de Always Encrypted con enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 568944db62ca94048c45450500d3060daa957680
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "74317939"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>Configuración y uso de Always Encrypted con enclaves seguros 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Always Encrypted con enclaves seguros](always-encrypted-enclaves.md) amplía la característica [Always Encrypted](always-encrypted-database-engine.md) existente para ofrecer una funcionalidad más completa en los datos confidenciales mientras mantiene la confidencialidad de estos. En este artículo se enumeran las tareas comunes para configurar y usar la característica.

Para ver un tutorial en el que se muestra cómo empezar a trabajar con Always Encrypted con enclaves seguros, consulte [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>Configuración del entorno para admitir enclaves y atestación
Para obtener detalles, vea los siguientes artículos:
- [Planificación de la atestación del Servicio de protección de host](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [Implementación del Servicio de protección de host para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [Registro del equipo con el Servicio de protección de host](./always-encrypted-enclaves-host-guardian-service-register.md)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Administración de claves para Always Encrypted con enclaves seguros
Consulte los artículos siguientes para más información:
- [Información general de la administración de claves para Always Encrypted con enclaves seguros](always-encrypted-enclaves-manage-keys.md)
- [Aprovisionamiento de claves habilitadas para el enclave](always-encrypted-enclaves-provision-keys.md)
- [Rotación de claves habilitadas para el enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>Configuración de columnas mediante Always Encrypted con enclaves seguros
Consulte los artículos siguientes para más información:
- [Información general de la configuración del cifrado de columna en contexto mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Configuración del cifrado de columnas en contexto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Uso de Always Encrypted con enclaves seguros para las columnas cifradas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> Para obtener un tutorial paso a paso sobre cómo configurar un entorno de prueba y probar la funcionalidad de Always Encrypted con enclaves seguros en SSMS, vea [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Consulta de columnas mediante Always Encrypted con enclaves seguros
Consulte los artículos siguientes para más información:
- [Información general de la consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS](always-encrypted-enclaves-query-columns.md)
- [Consulta de columnas mediante Always Encrypted con enclaves seguros con SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>Creación y uso de índices en columnas habilitadas para el enclave
Consulte los artículos siguientes para más información:
- [Creación y uso de índices en columnas mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desarrollo de aplicaciones mediante Always Encrypted con enclaves seguros
Consulte los artículos siguientes para más información:
- [Desarrollo de aplicaciones mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-client-development.md)
