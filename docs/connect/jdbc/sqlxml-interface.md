---
title: Interfaz SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 406c1c25c346680caba70c467e20e99df9977f13
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785843"
---
# <a name="sqlxml-interface"></a>Interfaz SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0, que presenta la interfaz java.sql.SQLXML. La interfaz SQLXML define métodos para interactuar con datos XML y manipularlos. El **SQLXML** tipo de datos se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml** tipo de datos.  
  
La interfaz SQLXML proporciona métodos para acceder al valor XML como un **cadena**, un **lector** o **escritor**, o como un **Stream**. También se puede acceder al valor XML mediante **Source** o establecerlo como **Result**, que se usan con las API del analizador XML, como Document Object Model (DOM), Simple API for XML (SAX) y Streaming API for XML (StAX), así como con las transformaciones XSLT y con XPath.  
  
## <a name="remarks"></a>Notas  

La tabla siguiente describe los métodos definidos en la interfaz SQLXML:  
  
|Sintaxis del método|Descripción del método|  
|-------------------|------------------------|  
|[void free()](http://go.microsoft.com/fwlink/?LinkId=131685)|Este método libera el objeto SQLXML y los recursos que contiene.|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|Devuelve un flujo de entrada para leer datos desde SQLXML.|  
|[Reader getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|Devuelve los datos **XML** como un objeto java.io.Reader o como un flujo de caracteres.|  
|[Extiende el T T origen getSource (clase\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|Devuelve un **origen** para leer el **XML** valor especificado por este **SQLXML** objeto.<br /><br /> **Nota:** El método getSource es compatible con los siguientes orígenes: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource y java.io.InputStream.|  
|[String getString()](http://go.microsoft.com/fwlink/?LinkId=131757)|Devuelve una representación de cadena del valor **XML** designado por este objeto SQLXML.|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|Recupera un flujo que se puede usar para escribir el valor **XML** que representa este objeto SQLXML.|  
|[Writer setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|Devuelve un flujo que se va a usar para escribir el valor **XML** que representa este objeto SQLXML.|  
|[Extiende el T T resultado setResult (clase\<T > resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|Devuelve un **resultado** para la configuración de la **XML** valor especificado por este **SQLXML** objeto.<br /><br /> **Nota:** El método setResult es compatible con los siguientes orígenes: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult y java.io.OutputStream.|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|Establece el valor XML designado por este objeto SQLXML para la representación **String** especificada.|  
  
Las aplicaciones pueden leer y escribir valores XML en o desde un objeto SQLXML solamente una vez.  
  
Cuando se llama al método free(), un objeto SQLXML se vuelve no válido y no puede ser leído ni escrito. Si la aplicación intenta invocar a un método que no sea free() en ese objeto SQLXML, se genera una excepción.  
  
El objeto SQLXML pasa a ser legible ni modificable cuando la aplicación llama a cualquiera de los siguientes métodos captador: getSource, getCharacterStream, getBinaryStream y getString.  
  
El objeto SQLXML se convierte en no leído ni escrito cuando la aplicación llama a cualquiera de los siguientes métodos establecedores: setResult, setCharacterStream, setBinaryStream y setString.  
  
## <a name="see-also"></a>Ver también  

[Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md)  
