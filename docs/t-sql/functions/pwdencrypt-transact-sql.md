---
title: PWDENCRYPT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PWDENCRYPT
- PWDENCRYPT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PWDENCRYPT function [Transact-SQL]
ms.assetid: 333e9a43-1099-4b9b-b941-4b0b016f47f3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e6e6ebf976f7fc475761685090064d14d00f6f75
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892133"
---
# <a name="pwdencrypt-transact-sql"></a>PWDENCRYPT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve el valor hash de la contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente al valor de entrada que usa la versión actual del algoritmo de hash de contraseñas.  
  
 PWDENCRYPT es una función antigua y puede que no se admita en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En cambio, puede usar [HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md). HASHBYTES proporciona más algoritmos de hash.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PWDENCRYPT ( 'password' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *password*  
 Es la contraseña que se va a cifrar. *password* es **sysname**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **varbinary(128)**  
  
## <a name="permissions"></a>Permisos  
 PWDENCRYPT está disponible al público.  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)  
  
  
