l# Kubernates Alıştırma


## Senaryo-1: Basit Bir Web Uygulaması Oluşturma ve Servisle İzole Etme
 Basit bir web uygulamasını bir Deployment, ReplicaSet ve bir ClusterIP tipi servis ile izole ederek Kubernetes üzerinde çalıştıracaksınız.İşte adımlar:
-	Basit bir Python veya Node.js web uygulaması oluşturun.
- Web uygulamanızı içeren bir Docker imajı oluşturun.
- Bir Deployment oluşturun ve bu imajı kullanarak uygulamanızı çalıştırın.
-	Bir ReplicaSet oluşturun ve ReplicaSet'in nasıl çalıştığını gözlemleyin.
-	Bir ClusterIP tipi Servis oluşturun ve bu servis üzerinden web uygulamanıza erişmeye çalışın.
-	Web uygulamanızın özel IP'sine servis üzerinden nasıl erişilebildiğini test edin.

Deployment oluşturmak için;

```bash
  kubectl create -f deployment-nodejs.yaml
```

Oluşturulan podları görüntülemek için;

```bash
  kubectl get pods
```

ClusterIP tipi servis manifest dosyasını oluşturmak için; 

```bash
  kubectl create -f service-nodejs.yaml
```
Oluşan servisi kontrol etmek için; 

```bash
  kubectl get services
```

## Senaryo-2: İki Ayrı Ortamda Uygulama Dağıtımı
Farklı birinci ve ikinci ortamlarda aynı uygulamayı dağıtarak ve dört ayrı Deployment kullanarak Kubernetes'te çalıştıracaksınız. İşte adımlar:
- Bir Python veya Node.js web uygulaması oluşturun.
- İki farklı Docker imajı oluşturun: "web-app:v1" ve "web-app:v2".
- İlk ortamda "web-app:v1" Docker imajını kullanarak bir Deployment ve Servis oluşturun.
- İkinci ortamda "web-app:v2" Docker imajını kullanarak aynı uygulamayı dağıtın.
- İlk ve ikinci ortamları izole eden iki farklı - ClusterIP tipi servis oluşturun.
- İki ortamda çalışan uygulamalara servisler üzerinden erişmeye çalışın ve sonuçları karşılaştırın.

Namespace oluşturmak için;

```bash
  kubectl create namespace uygulamav1
```
```bash
  kubectl create namespace uygulamav2
```

Oluşturulan namespace görüntülemek için;

```bash
  kubectl get ns
```

Deployment oluşturmak için;

```bash
  kubectl create deployment -f deployment-pythonv1.yaml
```
```bash
  kubectl create deployment -f deployment-pythonv2.yaml
```
Oluşan deploymentların namespacede çalıştığını kontrol etmek için; 

```bash
  kubectl get deployment -n uygulamav1
```
```bash
  kubectl get deployment -n uygulamav2
```
Servis manifest dosyası oluşturmak için; 

```bash
  kubectl create -f service-pythonv1.yaml
```
```bash
  kubectl create -f service-pythonv2.yaml
```
## Senaryo-3: Yük Dengelemeli ve Yüksek Erişilebilir Bir Uygulama Dağıtımı
 Yük dengelemeli ve yüksek erişilebilir bir uygulama dağıtımı oluşturarak Kubernetes becerilerinizi geliştirebilirsiniz. İşte adımlar:
- Uygulamanızı içeren bir Docker imajı oluşturun.
- Uygulamanızın yük dengelemesi için birden çok pod içeren bir Deployment oluşturun.
- Yük dengelemesi yapmak için bir LoadBalancer tipi Servis oluşturun (eğer bir bulut sağlayıcısını kullanıyorsanız, bu sağlayıcının yük dengeleyicisini kullanabilirsiniz).
- Uygulamanıza yük dengelemesi yapan LoadBalancer tipi servis üzerinden erişmeye çalışın ve yük dengesini test edin.
- Deployment'i manuel olarak ölçeklendirerek veya otomatik ölçekleme ile yüksek erişilebilirliği test edin.

Deployment oluşturmak için;

```bash
  kubectl create -f deployment-python.yaml
```

Oluşturulan podları görüntülemek için;

```bash
  kubectl get pods
```

ClusterIP tipi servis manifest dosyasını oluşturmak için; 

```bash
  kubectl create -f service-python.yaml
```
Oluşan servisi kontrol etmek için; 

```bash
  kubectl get services
```

Deployment'i manuel olarak ölçeklendirerek test etmek için; 

```bash
  kubectl scale deployment deployment-app-python --replicas=5
```
  
  
