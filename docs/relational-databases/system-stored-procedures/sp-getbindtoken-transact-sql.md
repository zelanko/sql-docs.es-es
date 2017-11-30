---
title: sp_getbindtoken (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_getbindtoken
- sp_getbindtoken_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_getbindtoken
ms.assetid: 5db87d77-85fa-45a3-a23a-3ea500f9a5ac
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58c73d303ac8fdcd8e9d4acf9f937538c3df816c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spgetbindtoken-transact-sql"></a>sp_getbindtoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un identificador único para la transacción. Este identificador único es una cadena que se utiliza para enlazar sesiones mediante sp_bindsession.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, utilice conjuntos de resultados activos múltiples (MARS) o transacciones distribuidas. Para obtener más información, vea [utilizando conjuntos de resultados activos múltiples &#40; MARS &#41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_getbindtoken [@out_token =] 'return_value' OUTPUT   
```  
  
## <a name="arguments"></a>Argumentos  
 [@out_token=]'*valor_devuelto*'  
 Es el token que se va a utilizar para enlazar las sesiones. *valor_devuelto* es **varchar (255)** no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 sp_getbindtoken devuelve un token válido solamente cuando el procedimiento almacenado se ejecuta dentro de una transacción activa. En caso contrario, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] devuelve un mensaje de error. Por ejemplo:  
  
```  
-- Declare a variable to hold the bind token.  
-- No active transaction.  
DECLARE @bind_token varchar(255);  
-- Trying to get the bind token returns an error 3921.  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
Server: Msg 3921, Level 16, State 1, Procedure sp_getbindtoken, Line 4  
Cannot get a transaction token if there is no transaction active.  
Reissue the statement after a transaction has been started.  
```  
  
 Cuando se utiliza sp_getbindtoken para dar de alta una conexión de transacción distribuida dentro de una transacción abierta, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve el mismo token. Por ejemplo:  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @bind_token varchar(255);  
  
BEGIN TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
  
BEGIN DISTRIBUTED TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 Las dos instrucciones `SELECT` devuelven el mismo símbolo (token):  
  
```  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
```  
  
 El símbolo (token) de enlace se puede utilizar con sp_bindsession para enlazar nuevas sesiones a la misma transacción. El símbolo (token) de enlace solo es válido localmente dentro de cada instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)], y no se puede compartir entre varias instancias.  
  
 Para obtener y pasar un símbolo (token) de enlace, debe ejecutar sp_getbindtoken antes de ejecutar sp_bindsession para compartir el mismo espacio de bloqueo. Si obtiene un símbolo (token) de enlace, sp_bindsession se ejecuta correctamente.  
  
> [!NOTE]  
>  Se recomienda utilizar la interfaz de programación de aplicaciones (API) de Servicios abiertos de datos srv_getbindtoken para obtener un símbolo (token) de enlace que se pueda utilizar desde un procedimiento almacenado extendido.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se obtiene un símbolo (token) de enlace y se muestra su nombre.  
  
```  
DECLARE @bind_token varchar(255);  
BEGIN TRAN;  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Token`  
  
 `----------------------------------------------------------`  
  
 `\0]---5^PJK51bP<1F<-7U-]ANZ`  
  
## <a name="see-also"></a>Vea también  
 [sp_bindsession &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [srv_getbindtoken &#40; Extendido API de procedimiento almacenado &#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)  
  
  
