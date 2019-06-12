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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ae50bcd5499ffa3bd5c10ef492d78de4685402e8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767216"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>Método getEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **Boolean** que indica si la propiedad encrypt está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si cifrar está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad encrypt se establece en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se asegura de que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el cifrado SSL para todos los datos que se envían entre el cliente y el servidor, si el servidor tiene un certificado instalado.  
  
 Si la propiedad de cifrado no se ha especificado o se ha establecido en **false**, el controlador no aplicará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para admitir el cifrado SSL. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se configura para exigir el cifrado SSL, se establece una conexión sin cifrado. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está configurada para exigir el cifrado SSL, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] habilitará automáticamente el cifrado SSL cuando se ejecute en una máquina virtual Java (JVM) configurada correctamente; de lo contrario, se finalizará la conexión y el controlador generará un error. Si no se establece la propiedad de cifrado, el método [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) devuelve el valor predeterminado **false**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
