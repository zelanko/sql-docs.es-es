---
title: CERT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CERT_ID
- CERT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ee18027e5c6c916f1ab3d0ca9c6bb501822c1d3b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="certid-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve el valor de identificador de un certificado.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
**'** *cert_name* **'**  

El nombre de un certificado de la base de datos.
  
## <a name="return-types"></a>Tipos de valores devueltos
 **int**  
  
## <a name="remarks"></a>Notas  
La vista de catálogo [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) muestra los nombres de certificados.
  
## <a name="permissions"></a>Permisos  
Es necesario tener los permisos apropiados en el certificado y que el autor de la llamada no tenga denegado el permiso VIEW DEFINITION en el certificado. Vea [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md#permissions) para obtener más información sobre los permisos de certificados.
  
## <a name="examples"></a>Ejemplos  
Este ejemplo devuelve el Id. de un certificado denominado `ABerglundCert3`.
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>Vea también
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
