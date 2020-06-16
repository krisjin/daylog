


https://github.com/Angel-ML/angel/issues/947 

    我司恰好有个项目用这个框架
    说下Json submit的心得

    在dnn以后，所有的submit都是graph submit，需要这两种类
    -Dangel.app.submit.class=com.tencent.angel.ml.core.graphsubmit.GraphRunner
    -Dml.model.class.name=com.tencent.angel.ml.core.graphsubmit.AngelModel \

    Graph定义在json中，
    --angel.ml.conf $daw_json_path
    坑一：不能用-Dangel.ml.conf $daw_json_path ,实测无效
    坑二： $daw_json_path 需要本地绝对路径

    graph构建：
    1）考虑特征数，max f
    2) 非零值 ， field num这个非常重要 fn
    3） embedding 大小k
    以deep fm为例，
    如果fn = 30，k=8，
    那么：embedding outputdim = 830 = 240
    如果是wide and deep
    同样需要考虑参数，比如C2(30) = 3029/2
    这个是一般初学者容易在shape中范的问题，导致模型跑不通

    我开始遇到这个坑，后来读afm paper在设置参数shape的时候想明白了，发现angel的dnn都需要注意shape的设置

    =====================
    因为这个框架没人回复，因此，作为热心用户，就互通有无了
    希望发扬共享精神，coding share
