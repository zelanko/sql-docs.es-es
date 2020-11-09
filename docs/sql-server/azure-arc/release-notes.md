---
title: 'SQL Server habilitado para Azure Arc: notas de la versión'
description: Notas de la versión más recientes
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 10/29/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3dcbc6b17d5abe87aabe923d70746d65595b9de6
ms.sourcegitcommit: dc3ea1696b8a4332934568439aed6cce4e9737eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244657"
---
# <a name="release-notes---azure-arc-enabled-sql-server-preview"></a>Notas de la versión: SQL Server habilitado para Azure Arc (versión preliminar)

> [!NOTE]
> Como característica en versión preliminar, la tecnología que se presenta en este artículo está sujeta a los [términos de uso complementarios para las versiones preliminares de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="september-2020"></a>Septiembre de 2020

SQL Server habilitado para Azure Arc se publica como versión preliminar pública. SQL Server habilitado para Azure Arc extiende los servicios de Azure a instancias de SQL Server hospedadas fuera de Azure en el centro de datos del cliente, en el sistema perimetral o en un entorno de varias nubes.

Para obtener más información, vea [SQL Server habilitado para Azure Arc (versión preliminar)](overview.md).

### <a name="known-issues"></a>Problemas conocidos

Los problemas siguientes se aplican a la versión de septiembre:

* La hoja **Register Azure Arc enabled SQL Server** (Registrar SQL Server habilitado para Azure Arc) no admite la configuración de etiquetas personalizadas. Para agregar etiquetas personalizadas, abra el recurso **SQL Server: Azure Arc** tras el registro y cambie las etiquetas de la página **Información general**.

* La conexión de instancias de SQL Server a Azure Arc requiere una cuenta que disponga de un amplio conjunto de permisos. Para obtener más información, vea [Permisos necesarios](overview.md#required-permissions).

## <a name="october-2020"></a>Octubre de 2020

La actualización de octubre incluye las mejoras siguientes:

* La hoja Register Azure Arc enabled SQL Server (Registrar SQL Server habilitado para Azure Arc) ahora incluye la pestaña **Etiquetas**. Las etiquetas se incluyen en el script de registro y se reflejan en los recursos **SQL Server: Azure Arc**. Para obtener más información, vea [Conexión de la instancia de SQL Server a Azure Arc](connect.md).

* La entrada **Estado del entorno** ahora admite la activación de **SQL Assessment** desde el portal mediante la implementación de una extensión *CustomScriptExtension*. Para obtener más información, vea [Configuración de SQL Assessment](assess.md#run-on-demand-sql-assessment).

### <a name="known-issues"></a>Problemas conocidos

Los problemas siguientes se aplican a la versión de octubre:

* La conexión de instancias de SQL Server a Azure Arc requiere una cuenta que disponga de un amplio conjunto de permisos. Para obtener más información, vea [Permisos necesarios](overview.md#required-permissions).

## <a name="next-steps"></a>Pasos siguientes

**¿Solo desea realizar algunas pruebas?**  Empiece a trabajar rápidamente con el [inicio rápido de SQL Server habilitado para Azure Arc](https://aka.ms/AzureArcSqlServerJumpstart).
