---
title: Método getEncrypt (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7edee23f7111b55a6d34ac6ae10bf3720879fc01
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219309"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>Método getEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **Boolean** que indica si la propiedad encrypt está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si está habilitado el cifrado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se asegura de que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el cifrado TLS para todos los datos que se envían entre el cliente y el servidor, si el servidor tiene un certificado instalado.  
  
 Si la propiedad encrypt no se ha especificado o se ha establecido en **false**, el controlador no aplicará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para admitir el cifrado TLS. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se configura para exigir el cifrado TLS, se establece una conexión sin cifrado. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está configurada para exigir el cifrado TLS, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] habilita automáticamente el cifrado TLS cuando se ejecuta en una máquina virtual Java (JVM) configurada correctamente; de lo contrario, se finaliza la conexión y el controlador genera un error. Si no se establece la propiedad de cifrado, el método [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) devuelve el valor predeterminado **false**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
