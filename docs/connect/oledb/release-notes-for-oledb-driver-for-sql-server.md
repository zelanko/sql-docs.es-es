---
title: Notas de la versión (Controlador OLE DB para SQL Server) | Microsoft Docs
ms.date: 02/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2a1d6d216f4f7ec7fee0f5f9aa5810c78f1936e6
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161772"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de la versión del controlador Microsoft OLE DB para SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Esta página describe lo que se ha agregado en cada versión del controlador de Microsoft OLE DB para SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1821"></a>18.2.1

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

Febrero de 2019

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la codificación UTF-8 del servidor. | &bull; &nbsp; [Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Soporte técnico de la autenticación de Azure Active Directory. | &bull; &nbsp; [Uso de Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Julio de 2018

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la `UseFMTONLY` palabra clave de cadena de conexión y para el `SSPROP_INIT_USEFMTONLY` propiedad de inicialización. | `UseFMTONLY` controla cómo se recuperan los metadatos cuando se conecta a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones más recientes.<br/><br/>&bull; &nbsp; [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Errores corregidos

| Error corregido | Detalles |
| :-------- | :------ |
| Fijo versión incorrecta del archivo de formato BCP. | Las versiones 18.0 controlador OLE DB establece incorrectamente la versión del archivo de formato BCP para 18.0, en lugar de en 11.0.<br/><br/>No se pueden leer los archivos de formato generados por las versiones 18.0 controlador OLE DB 18.1 de controlador de OLE DB.<br/><br/>Si tiene que usar los archivos de formato generados por la versión anterior del controlador con el nuevo controlador, puede editar manualmente los archivos para cambiar la versión 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la `MultiSubnetFailover` palabra clave de cadena de conexión y el `SSPROP_INIT_MULTISUBNETFAILOVER` propiedad de inicialización. | &bull; &nbsp; [Compatibilidad del controlador OLE DB para SQL Server con la alta disponibilidad y la recuperación ante desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vea también

[Controlador Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
