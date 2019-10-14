---
title: Opción de configuración del servidor external scripts enabled | Microsoft Docs
ms.date: 11/13/2017
ms.prod: sql
ms.technology: configuration
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3f47352cc82ac831ebcd64548baa24423490094f
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006048"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>Opción de configuración del servidor external scripts enabled
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] y [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Utilice la opción **external scripts enabled** para habilitar la ejecución de scripts con determinadas extensiones de lenguaje remoto. Esta propiedad está DESACTIVADA de forma predeterminada. El programa de instalación, opcionalmente, puede establecer esta propiedad en true si **Advanced Analytics Services** (Servicios de análisis avanzado) está instalado.

## <a name="remarks"></a>Notas

Debe habilitar la opción de script externo habilitado antes de poder ejecutar un script externo mediante el procedimiento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) . Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible, como R o Python. 

+ Para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] es compatible con el lenguaje R en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y un conjunto de herramientas de estación de trabajo y bibliotecas de conectividad de R.

    Instale la característica **Extensiones de análisis avanzado** durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar la ejecución de los scripts de R. El lenguaje R se instala de manera predeterminada.

+ Para [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] usa la misma arquitectura que en SQL Server 2016, pero es compatible con el lenguaje Python.

    Instale la característica **Extensiones de análisis avanzado** durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar la ejecución de scripts externos. No olvide seleccionar al menos un lenguaje durante la instalación inicial: R, Python o ambos. 

## <a name="additional-requirements"></a>Requisitos adicionales

Después de la instalación, ejecute el script siguiente para habilitar los scripts externos:

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

Debe reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que este cambio surta efecto.

Para obtener más información, consulte [Set up SQL Server Machine Learning](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md) (Configurar SQL Server Machine Learning).

## <a name="see-also"></a>Vea también

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)

[sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

[Servicios de aprendizaje de máquina SQL Server](../../advanced-analytics/r/sql-server-r-services.md)
