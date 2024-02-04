
# React-Queue-State-Updates

## Queueing a Series of State Updates Nedir?

Bu proje, React uygulamalarında durumu güncellemek için bir kuyruk mekanizması kullanarak state güncellemelerini düzenleyen bir mimari sunar. Bu, özellikle ardışık state güncellemeleri yaparken, performansı artırmak ve beklenmeyen sonuçları önlemek amacıyla kullanışlıdır.

## Nasıl Bir Mimaride Çalışır?

React-Queue-State-Updates, state güncellemelerini bir kuyrukta toplar ve uygun bir zaman aralığında tek bir işlem olarak gerçekleştirir. Bu, ardışık güncellemeleri birleştirerek performans avantajı sağlar ve uygulamanın daha akıcı çalışmasına yardımcı olur.

## Dikkat Edilmesi Gereken Şeyler

- Kuyruk, işlemleri sırayla gerçekleştirdiği için, asenkron operasyonlarda dikkatli olunmalıdır.
- Kuyruk, genellikle kullanıcının etkileşimlerini işlemek için kullanılan event handler'larla entegre edilmelidir.

## Faydaları

- Ardışık state güncellemelerini birleştirerek gereksiz render işlemlerini önler.
- Performansı artırır ve uygulamanın daha akıcı çalışmasını sağlar.
- Kuyruk mekanizması, state güncellemelerini düzenleyerek beklenmeyen hataları önlemeye yardımcı olur.


```javascript
import { useState } from 'react';

export default function RequestTracker() {
  const [pending, setPending] = useState(0);
  const [completed, setCompleted] = useState(0);

  async function handleClick() {
    setPending(p=> p + 1);  // Bir güncelleyici fonksiyon gibi davranır. 
    await delay(3000);  // Bir Gecikme sağlayıcısıdır. 3 saniye gecikme verir.
    setPending(p=> p - 1); // Burada ki "p" değeri pending'i gösteriyor üst satırlarda belirtilen değer pending de depolanıyor ve bu satırda p - 1 yani pending - 1 olmuş oluyor.
    setCompleted(c=> c + 1);  // Bu satır da completed değerini artırmaya yönekik bir kod yazmış bulunuyoruz.
  }

  return (
    <>
      <h3>
        Pending: {pending}
      </h3>
      <h3>
        Completed: {completed}
      </h3>
      <button onClick={handleClick}>
        Buy     
      </button>
    </>
  );
}

function delay(ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms);
  });
}
