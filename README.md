**internal-service-0.1.0**

helm install flask-app mycharts/internal-service
--namespace flask-app-ns
--create-namespace
--set replicaCount=1
--set service.type=LoadBalancer
--set service.port=80
--set app.containerPort=8000
--set app.name=flask-app

**NGINX without TLS, wildcard host**

<pre class="overflow-visible!" data-start="2562" data-end="2686"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre! language-bash"><span><span>helm install flask-app ./internal-service \
  --</span><span>set</span><span> ingress.controller=nginx \
  --</span><span>set</span><span> ingress.tls.enabled=</span><span>false</span><span>
</span></span></code></div></div></pre>

**ALB with TLS & ACM**

<pre class="overflow-visible!" data-start="2712" data-end="2950"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre! language-bash"><span><span>helm install flask-app ./internal-service \
  --</span><span>set</span><span> ingress.controller=alb \
  --</span><span>set</span><span> ingress.tls.enabled=</span><span>true</span><span> \
  --</span><span>set</span><span> ingress.tls.acmArn=arn:aws:acm:region:account:certificate/cert-id \
  --</span><span>set</span><span> ingress.host=myapp.example.com
</span></span></code></div></div></pre>

**NodePort Service with NGINX**

<pre class="overflow-visible!" data-start="2985" data-end="3166"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre! language-bash"><span><span>helm install flask-app ./internal-service \
  --</span><span>set</span><span> service.type=NodePort \
  --</span><span>set</span><span> service.port=8080 \
  --</span><span>set</span><span> service.nodePort=30090 \
  --</span><span>set</span><span> ingress.controller=nginx</span></span></code></div></div></pre>
