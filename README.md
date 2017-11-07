  
# PerfAILibs

## Performance Analysis OpenAI-gemm vs cuBLAS on GEMM

### OpenAI-gemm vs CUDA8.0.61 on TitanXp

 python2.7.5 
 1) install pip
    wget https://bootstrap.pypa.io/get-pip.py
    python get-pip.py
4) install pycuda (three method)
 a) pip install pycuda (work)
 b) apt-get install python-cuda( not good)
 c) dowload pycuda source code // pycuda-2017.1.1.tar.gz
    configure: python configure.py --cuda-root=/usr/local/cuda/
    make
    make install
   
    Test the install of pycuda:
    $python test/test_driver.py
 
3）Nervana NEON
   https://github.com/NervanaSystems/neon.git 
  cd neon
  make
  . .venv/bin/activate
  
  Test: python examples/mnist_mlp.py
  
4） git clone https://github.com/openai/openai-gemm.git

  
  
TITAN Xp


|     M|     N|     K| Op|OpenAI_32|cuBLAS_32|ratio_32|OpenAI_16|cuBLAS_16|ratio_16|
|------|------|------|---|---------|---------|--------|---------|---------|--------|
|    16|  1760|  1760| NN|     2968|     2005|     1.5|     3755|      346|    10.9| 
|    32|  1760|  1760| NN|     5740|     1170|     4.9|     7224|      532|    13.6| 
|    64|  1760|  1760| NN|     6711|     4445|     1.5|     8032|     3007|     2.7| 
|   128|  1760|  1760| NN|     7142|     6813|     1.0|     9908|     5472|     1.8| 
|  7000|  1760|  1760| NN|    12496|     9934|     1.3|    11026|    10222|     1.1| 
|    16|  2048|  2048| NN|     2899|     1561|     1.9|     3906|      265|    14.7| 
|    32|  2048|  2048| NN|     5669|     1380|     4.1|     6763|      618|    10.9|
|    64|  2048|  2048| NN|     7356|     2985|     2.5|     8690|     3316|     2.6|
|   128|  2048|  2048| NN|     8765|     5810|     1.5|     9139|     5086|     1.8|
|  7000|  2048|  2048| NN|    10909|    10238|     1.1|    11081|    10193|     1.1|
|    16|  2560|  2560| NN|     3137|     1538|     2.0|     4808|      257|    18.7|
|    32|  2560|  2560| NN|     6262|     1667|     3.8|     7956|      760|    10.5|
|    64|  2560|  2560| NN|     7711|     3401|     2.3|     8987|     3918|     2.3|
|   128|  2560|  2560| NN|     7957|     5798|     1.4|     9737|     6097|     1.6|
|  7000|  2560|  2560| NN|    10819|    10246|     1.1|    11604|     9914|     1.2|
|    16|  4096|  4096| NN|     2964|     1381|     2.1|     4940|      278|    17.7|
|    32|  4096|  4096| NN|     5827|     2273|     2.6|     8531|      767|    11.1|
|    64|  4096|  4096| NN|     8203|     4008|     2.0|    10249|     1064|     9.6|
|   128|  4096|  4096| NN|     8583|     5254|     1.6|    10065|     5490|     1.8|
|  7000|  4096|  4096| NN|    11026|    10215|     1.1|    11927|    10324|     1.2|
|    16|  1760|  1760| NT|     1875|     1169|     1.6|     2943|      312|     9.4|
|    32|  1760|  1760| NT|     3659|     1436|     2.5|     5733|      465|    12.3|
|    64|  1760|  1760| NT|     6034|     2103|     2.9|     7583|     1875|     4.0|
|   128|  1760|  1760| NT|     7130|     4060|     1.8|     9546|     3589|     2.7|
|  7000|  1760|  1760| NT|    10552|     9886|     1.1|    10565|    10106|     1.0|
|    16|  2048|  2048| NT|     2735|     1357|     2.0|     3942|      309|    12.7|
|    32|  2048|  2048| NT|     5345|     1345|     4.0|     6006|      495|    12.1|
|    64|  2048|  2048| NT|     7110|     2158|     3.3|     8275|     2628|     3.1|
|   128|  2048|  2048| NT|     8453|     5289|     1.6|     9283|     5013|     1.9|
|  7000|  2048|  2048| NT|    10234|     9957|     1.0|    10686|     9949|     1.1|
|    16|  2560|  2560| NT|     2139|     1367|     1.6|     3623|      341|    10.6|
|    32|  2560|  2560| NT|     4143|     1531|     2.7|     5791|      612|     9.5|
|    64|  2560|  2560| NT|     7033|     1784|     3.9|     8152|     2375|     3.4|
|   128|  2560|  2560| NT|     7880|     3522|     2.2|     9706|     5461|     1.8|
|  7000|  2560|  2560| NT|    10366|     9622|     1.1|    11393|     9869|     1.2|
|    16|  4096|  4096| NT|     2891|     1595|     1.8|     4556|      367|    12.4|
|    32|  4096|  4096| NT|     5729|     2324|     2.5|     7741|      763|    10.1|
|    64|  4096|  4096| NT|     7576|     3743|     2.0|     5834|      833|     7.0|
|   128|  4096|  4096| NT|     4958|     3471|     1.4|     6143|     3484|     1.8|
|  7000|  4096|  4096| NT|     8646|     4713|     1.8|     6918|     6326|     1.1|
|  7133|  1760|  1760| TN|     6186|     7634|     0.8|     6690|     6353|     1.1|
|  7133|  2048|  2048| TN|     6683|     6503|     1.0|    10948|     6758|     1.6|
|  7133|  2560|  2560| TN|     6541|     6617|     1.0|     6756|     6702|     1.0|
|  7133|  4096|  4096| TN|     6733|     6614|     1.0|     6905|     6820|     1.0|
|  9124|  5124|  1760| NN|     6402|     6239|     1.0|     7430|     6154|     1.2|
|  9124|  5124|  2048| NN|     6375|     6200|     1.0|     6676|     6392|     1.0|
|  9124|  5124|  2560| NN|     6383|     6163|     1.0|     6989|     6256|     1.1|
|  9124|  5124|  4096| NN|     6334|     6155|     1.0|     7804|     6357|     1.2|
|  9124|  5124|  1760| NT|     5916|     2337|     2.5|     6411|     6007|     1.1|
|  9124|  5124|  2048| NT|     6180|     4377|     1.4|     9030|     6109|     1.5|
|  9124|  5124|  2560| NT|     6789|     2247|     3.0|     6456|     6021|     1.1|
|  9124|  5124|  4096| NT|     6247|     4031|     1.5|     6635|     6184|     1.1|
|  8457|    35|  1760| NN|     2618|      721|     3.6|     2650|      533|     5.0|
|  8457|    35|  2048| NN|     2439|     1358|     1.8|     3123|      485|     6.4|
|  8457|    35|  2560| NN|     3844|      702|     5.5|     3839|      486|     7.9|
|  8457|    35|  4096| NN|     2445|     1855|     1.3|     3366|      549|     6.1|
|  8457|    35|  1760| NT|     2412|     1315|     1.8|     2620|      758|     3.5|
|  8457|    35|  2048| NT|     3045|     2743|     1.1|     3036|      770|     3.9|
|  8457|    35|  2560| NT|     2491|     1360|     1.8|     3141|      772|     4.1|
|  8457|    35|  4096| NT|     4075|     2164|     1.9|     3229|      914|     3.5|
|    16|  7680|  2560| NN|     1773|      486|     3.7|     3248|      216|    15.0|
|    32|  7680|  2560| NN|     3540|     2324|     1.5|     5606|      805|     7.0|
|    64|  7680|  2560| NN|     4436|     3892|     1.1|     5958|      924|     6.5|
|   128|  7680|  2560| NN|     6206|     6204|     1.0|    11228|     6390|     1.8|
|    16|  7680|  2560| NT|     1237|      933|     1.3|     2928|      186|    15.7|
|    32|  7680|  2560| NT|     2498|     1292|     1.9|     4445|      723|     6.1|
|    64|  7680|  2560| NT|     4009|     2507|     1.6|     5732|     1209|     4.7|
|   128|  7680|  2560| NT|     4944|     2479|     2.0|     5924|     4813|     1.2|
|    16|  3072|  1024| NN|     1516|      849|     1.8|     2646|      170|    15.6|
|    32|  3072|  1024| NN|     3962|     1117|     3.5|     3805|      514|     7.4|
|    64|  3072|  1024| NN|     3852|     1905|     2.0|     4745|      668|     7.1|
|   128|  3072|  1024| NN|     5037|     3804|     1.3|     5430|     4271|     1.3|
|    16|  3072|  1024| NT|     1561|      652|     2.4|     3404|      141|    24.1|
|    32|  3072|  1024| NT|     3087|      948|     3.3|     3418|      413|     8.3|
|    64|  3072|  1024| NT|     4099|     2414|     1.7|     4901|      741|     6.6|
|   128|  3072|  1024| NT|     4603|     3533|     1.3|     5482|     4271|     1.3|
|  7435|  3072|  1024| TN|     5963|    10749|     0.6|     6962|     6559|     1.1|
|  5481|  7680|  2560| TN|     6602|     6553|     1.0|     6918|     6242|     1.1


### OpenAI-gemm vs CUDAV9.0.176 on TitanXp
 a）Install NVIDIA GPU Driver
 b）Install cuda9.0
 c）install pycuda with command
    pip install pycuda // the version of pycuda is 2017.1.1
 d) Install neon
    https://github.com/NervanaSystems/neon.git
    make
    . .venv/bin/activate

Tips: when install python with anaconda2, install python virtualenv with below comman
$conda install virtualenv

e) Download the openai-gemm  
   git clone https://github.com/openai/openai-gemm.git  
 
   Tips: The ptxas of cuda9.0 will introduce bugs when compile  "sgemm_128x128x8_NN.ptx"  
   Hacks: 
   replace ptxas with ptaas of cuda-8.0, such as below:
 
    run_command([ "/usr/local/cuda-8.0/bin/ptxas -v -arch", arch, "-o", cubin_file, ptx_file, ";" ] + maxas_i + [sass_file, cubin_file])

 
 
TITAN Xp


|     M|     N|     K| Op|OpenAI_32|cuBLAS_32|ratio_32|OpenAI_16|cuBLAS_16|ratio_16|
|------|------|------|---|---------|---------|--------|---------|---------|--------|
|    16|  1760|  1760| NN|     2945|     2946|     1.0|     3766|     2504|     1.5|
|    32|  1760|  1760| NN|     5780|     5733|     1.0|     7171|     7013|     1.0|
|    64|  1760|  1760| NN|     6658|     6069|     1.1|     8091|     7806|     1.0|
|   128|  1760|  1760| NN|     7113|     6611|     1.1|     9803|     9195|     1.1|
|  7000|  1760|  1760| NN|    10862|    10585|     1.0|    11074|    10637|     1.0|
|    16|  2048|  2048| NN|     2886|     2883|     1.0|     3917|     1968|     2.0|
|    32|  2048|  2048| NN|     5688|     5637|     1.0|     6775|     6658|     1.0|
|    64|  2048|  2048| NN|     7199|     4942|     1.5|     8656|     8252|     1.0|
|   128|  2048|  2048| NN|     8497|     6691|     1.3|     9856|     8669|     1.1|
|  7000|  2048|  2048| NN|    11166|    10721|     1.0|    11491|    10757|     1.1|
|    16|  2560|  2560| NN|     3175|     3175|     1.0|     4798|     1984|     2.4|
|    32|  2560|  2560| NN|     6259|     6241|     1.0|     8015|     7678|     1.0|
|    64|  2560|  2560| NN|     7690|     6057|     1.3|     8967|     8787|     1.0|
|   128|  2560|  2560| NN|     8083|     8065|     1.0|    10221|     9269|     1.1|
|  7000|  2560|  2560| NN|    10977|    10630|     1.0|    11492|    10144|     1.1|
|    16|  4096|  4096| NN|     2986|     2985|     1.0|     4982|     2113|     2.4|
|    32|  4096|  4096| NN|     5844|     5747|     1.0|     8560|     7715|     1.1|
|    64|  4096|  4096| NN|     8395|     7038|     1.2|    10255|     8941|     1.1|
|   128|  4096|  4096| NN|     8301|     8800|     0.9|    10613|     9685|     1.1|
|  7000|  4096|  4096| NN|    11127|    10689|     1.0|    12064|    10606|     1.1|
|    16|  1760|  1760| NT|     1908|     1908|     1.0|     2958|     1442|     2.1|
|    32|  1760|  1760| NT|     3837|     3838|     1.0|     5680|     4004|     1.4|
|    64|  1760|  1760| NT|     5893|     5614|     1.0|     7650|     6147|     1.2|
|   128|  1760|  1760| NT|     6958|     6281|     1.1|     9327|     8775|     1.1|
|  7000|  1760|  1760| NT|    10628|     9951|     1.1|    11320|    10339|     1.1|
|    16|  2048|  2048| NT|     2805|     2807|     1.0|     3874|     1666|     2.3|
|    32|  2048|  2048| NT|     5537|     5516|     1.0|     6163|     5891|     1.0|
|    64|  2048|  2048| NT|     6923|     3580|     1.9|     8280|     7984|     1.0|
|   128|  2048|  2048| NT|     8487|     5545|     1.5|     9799|     9107|     1.1|
|  7000|  2048|  2048| NT|    10352|    10457|     1.0|    10676|    10284|     1.0|
|    16|  2560|  2560| NT|     2149|     2144|     1.0|     3557|     1608|     2.2|
|    32|  2560|  2560| NT|     4218|     4212|     1.0|     5882|     4237|     1.4|
|    64|  2560|  2560| NT|     6881|     2297|     3.0|     8156|     7268|     1.1|
|   128|  2560|  2560| NT|     7823|     4053|     1.9|     9593|     9244|     1.0|
|  7000|  2560|  2560| NT|    10173|    10022|     1.0|    11360|     9892|     1.1|
|    16|  4096|  4096| NT|     2912|     2915|     1.0|     4612|     1885|     2.4|
|    32|  4096|  4096| NT|     5661|     5601|     1.0|     8568|     6064|     1.4|
|    64|  4096|  4096| NT|     8277|     4035|     2.1|     9800|     8899|     1.1|
|   128|  4096|  4096| NT|     8478|     5618|     1.5|    10338|     8550|     1.2|
|  7000|  4096|  4096| NT|    10782|    10468|     1.0|    11480|    10310|     1.1|
|  7133|  1760|  1760| TN|    10469|    10784|     1.0|    10813|     9808|     1.1|
|  7133|  2048|  2048| TN|    10301|    11261|     0.9|    11195|     9929|     1.1|
|  7133|  2560|  2560| TN|    11057|    11083|     1.0|    11533|    10716|     1.1|
|  7133|  4096|  4096| TN|    11152|    11140|     1.0|    11852|    10993|     1.1|
|  9124|  5124|  1760| NN|    10530|    10642|     1.0|    11319|    10615|     1.1|
|  9124|  5124|  2048| NN|    10604|    10588|     1.0|    11423|    10609|     1.1|
|  9124|  5124|  2560| NN|    10669|    10553|     1.0|    11460|    10574|     1.1|
|  9124|  5124|  4096| NN|    10628|    10548|     1.0|    11433|    10561|     1.1|
|  9124|  5124|  1760| NT|     9817|     9634|     1.0|    11027|     9829|     1.1|
|  9124|  5124|  2048| NT|    10321|    10309|     1.0|    11240|    10274|     1.1|
|  9124|  5124|  2560| NT|     9487|     9499|     1.0|    11061|     9399|     1.2|
|  9124|  5124|  4096| NT|    10500|    10361|     1.0|    11162|    10458|     1.1|
|  8457|    35|  1760| NN|     3846|     3850|     1.0|     4580|     4587|     1.0|
|  8457|    35|  2048| NN|     4097|     4100|     1.0|     5149|     5423|     0.9|
|  8457|    35|  2560| NN|     3952|     3988|     1.0|     4555|     4550|     1.0|
|  8457|    35|  4096| NN|     4139|     4136|     1.0|     5204|     5746|     0.9|
|  8457|    35|  1760| NT|     4250|     4236|     1.0|     4554|     4547|     1.0|
|  8457|    35|  2048| NT|     4924|     4965|     1.0|     5206|     5217|     1.0|
|  8457|    35|  2560| NT|     4295|     4301|     1.0|     4381|     4381|     1.0|
|  8457|    35|  4096| NT|     4929|     4900|     1.0|     5438|     5433|     1.0|
|    16|  7680|  2560| NN|     3102|     3074|     1.0|     5808|     1499|     3.9|
|    32|  7680|  2560| NN|     6166|     6134|     1.0|     9251|     8751|     1.1|
|    64|  7680|  2560| NN|     7452|     8127|     0.9|     9362|     9273|     1.0|
|   128|  7680|  2560| NN|    11010|     8898|     1.2|    10782|     9975|     1.1|
|    16|  7680|  2560| NT|     2207|     2209|     1.0|     4233|     1636|     2.6|
|    32|  7680|  2560| NT|     4302|     4302|     1.0|     7817|     4267|     1.8|
|    64|  7680|  2560| NT|     7021|     2204|     3.2|     9709|     7155|     1.4|
|   128|  7680|  2560| NT|     8197|     3210|     2.6|     9996|     9436|     1.1|
|    16|  3072|  1024| NN|     2640|     2440|     1.1|     3876|     2042|     1.9|
|    32|  3072|  1024| NN|     5095|     4706|     1.1|     6342|     6027|     1.1|
|    64|  3072|  1024| NN|     6679|     5293|     1.3|     8210|     7982|     1.0|
|   128|  3072|  1024| NN|     8581|     6583|     1.3|     9501|     8927|     1.1|
|    16|  3072|  1024| NT|     2611|     2340|     1.1|     3842|     1380|     2.8|
|    32|  3072|  1024| NT|     5103|     4582|     1.1|     5764|     4728|     1.2|
|    64|  3072|  1024| NT|     6600|     3392|     1.9|     8152|     8020|     1.0|
|   128|  3072|  1024| NT|     7607|     5986|     1.3|     9369|     8936|     1.0|
|  7435|  3072|  1024| TN|    10902|    10756|     1.0|    10892|    10028|     1.1|
|  5481|  7680|  2560| TN|    10926|    10944|     1.0|    11673|    11198|     1.0|
