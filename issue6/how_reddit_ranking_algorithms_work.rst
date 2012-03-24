Reddit �����㷨�Ĺ���ԭ��
==================================

ԭ�ģ� `<http://eli.thegreenplace.net/2012/03/15/processing-xml-in-python-with-elementtree/>`_

���ߣ� `Tiezhen WANG <https://github.com/wangtz>`_ 

.. figure:: http://amix.dk/uploads/reddit.png
   :align: center
   :alt: Reddit Icon

��ƪ�� `Hacker News �����㷨�Ĺ���ԭ�� <http://amix.dk/blog/post/19574>`_ һ�ĵ����ƪ�������Ҫ������ `Reddit <http://www.reddit.com/>`_ ����ζԻ���ͻظ���������ġ�Reddit �������㷨�����Ƿǳ���������ʵ�ֵģ���������������һЩ��̽�֡�

��һ������Ҫ�ǶԻ������������ۣ����� Reddit ����ζԻ�����������ġ����������������������ۣ�Reddit �Ի��������ʹ���˲�ͬ�������㷨 (��һ���
`Hacker News <http://news.ycombinator.com/>`_ ��̫һ��), Reddit �����������㷨�Ǻ�ֵ����ζ�ģ����� Randall
Munroe (`xkcd <http://xkcd.com/>`_ ������) ���.

�ӻ��������㷨��ʵ��˵����
~~~~~~~~~~~~~~~~~~~~~~~~~~

Reddit ���������ǵĴ��룬�ܷ�������ҵ���Reddit ���� Python ʵ�ֵģ�Դ������ `���� <http://code.reddit.com/>`_. �����㷨ʹ����
`Pyrex <http://www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex/>`_ (һ������д Python �� C ��չ������) ��������ܡ�����Ϊ�˷���˵�������� Python д�� `���ǵ� Pyrex ���� <http://code.reddit.com/browser/r2/r2/lib/db/_sorts.pyx>`_.

����㷨������������ (hot ranking),��������:

::

    #Rewritten code from /r2/r2/lib/db/_sorts.pyx

    from datetime import datetime, timedelta
    from math import log

    epoch = datetime(1970, 1, 1)

    def epoch_seconds(date):
        """Returns the number of seconds from the epoch to date."""
        td = date - epoch
        return td.days * 86400 + td.seconds + (float(td.microseconds) / 1000000)

    def score(ups, downs):
        return ups - downs

    def hot(ups, downs, date):
        """The hot formula. Should match the equivalent function in postgres."""
        s = score(ups, downs)
        order = log(max(abs(s), 1), 10)
        sign = 1 if s > 0 else -1 if s < 0 else 0
        seconds = epoch_seconds(date) - 1134028003
        return round(order + sign * seconds / 45000, 7)

һ��������ѧ���ԶԸ��㷨������ (������ `SEOmoz <http://www.seomoz.org/blog/reddit-stumbleupon-delicious-and-hacker-news-algorithms-exposed>`_ ������������ģ����ǲ�ȷ�����Ƿ�������ԭ����):

.. figure:: http://amix.dk/uploads/reddit_cf_algorithm.png
   :align: center
   :alt: Reddit ʹ�õ��㷨

����ʱ���Ӱ��
~~~~~~~~~~~~~~

����ʱ��ͻ���������Ӱ����Ա���������:

-  ����ʱ��������кܴ�Ӱ�죬���㷨ʹ���µĻ���ȾɵĻ���������ǰ
-  ����ĵ÷ֲ�����Ϊʱ�����ʧ�����٣������µĻ����ȾɵĻ���÷ָߡ����� Hacker New ���㷨��ͬ (����ʱ��ķ�չ���ͻ���ĵ÷�)

��ͼչʾ�˻���÷��ں����Ͳ�������������ʱ������ʱ����仯�������

.. figure:: http://amix.dk/uploads/reddit_score_time.png
   :align: center
   :alt: Reddit �Ļ���÷�

������ϵ
~~~~~~~~

Reddit ���������㷨ʹ���˶�������������ǰ���ͶƱ������ͶƱ�Ĳ�ࣺ

-  ǰʮ��������֮���100����1000��ͶƱ����ͬ��Ȩ�ء�

�μ������ͼ:

.. figure:: http://amix.dk/uploads/reddit_log_function.png
   :align: center
   :alt: ��������������Ӱ��

ȥ����������֮����ע���������Ժ�������Ч��

.. figure:: http://amix.dk/uploads/reddit_without_log.png
   :align: center
   :alt: ���û�ж�������

����Ʊ��Ӱ��
~~~~~~~~~~~~~~~~~~~~

Reddit ��Ϊ������ļ�������Ͷ����Ʊ����վ�������ϱߴ���������һ������ĵ÷ֱ�����ɣ������� - ������

�±ߵ�ͼ���԰���������⣺

.. figure:: http://amix.dk/uploads/reddit_up_down.png
   :align: center
   :alt: ������Ӱ��

��һ�����Щͬʱ�д����޳ɺͷ���Ʊ�Ļ��⣨����˵һЩ������Ļ��⣩������Ӱ�졣���ֻ�����������ֻ���޳�Ʊ�Ļ����һЩ����Ҳ�ͽ�����Ϊʲô kittens ������һЩû������Ļ���������˿�ǰ��

���������㷨�Ľ���
~~~~~~~~~~~~~~~~~~

-  ����ʱ����һ���ǳ���Ҫ�Ĳ�����ͨ�����µĻ���Ҫ�ȾɵĻ���������ǰ
-  ǰ10����������������100������ͬ����Ȩ�ء�����һ������10�������Ļ��⣬����50�������Ļ����������Ƶ�����
-  ������Ļ��⣨֧��Ʊ�ͷ���Ʊ�����������Ҫ��֧��Ʊռ������Ļ�����������

����̸һ�� Reddit �����������㷨
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Reddit ���������㷨����xkcd �� `Randall Munroe <http://xkcd.com/>`_ ����ġ�������ƪ��������ؽ����������㷨:

-  `reddit �µ����������㷨 <http://blog.reddit.com/2009/10/reddits-new-comment-sorting-system.html>`_

���ݿ��Թ������£�

-  �������㷨���ʺ�Ӧ�������ۣ���Ϊ����ƫ�������ڷ��������
-  ���۵������㷨Ӧ���뷢��ʱ���޹�
-  Edwin B. Wilson ��1927�������һ�������������������ѷ�÷����� (Wilson score interval)�������Ա������������� (The confidence sort)
-  ���������ͶƱ������һ������Ķ�������ͶƱ����ĳ���ͳ�ƣ�������һ��ͶƱѡ��
-  `��ô���������ͶƱƽ��ֵ���� <http://www.evanmiller.org/how-not-to-sort-by-average-rating.html>`_ ��������ν����������򣬷ǳ��Ƽ��Ķ���

����������������
~~~~~~~~~~~~~~~~

`\_sorts.pyx <http://code.reddit.com/browser/r2/r2/lib/db/_sorts.pyx>`_ ʵ�������������㷨�����Ѿ��ô� Python ����ʵ����ԭ���� Pyrex ���룬�����Ż���صĴ���Ҳ��ʡ���ˡ�

::

    #Rewritten code from /r2/r2/lib/db/_sorts.pyx

    from math import sqrt

    def _confidence(ups, downs):
        n = ups + downs

        if n == 0:
            return 0

        z = 1.0 #1.0 = 85%, 1.6 = 95%
        phat = float(ups) / n
        return sqrt(phat+z*z/(2*n)-z*((phat*(1-phat)+z*z/(4*n))/n))/(1+z*z/n)

    def confidence(ups, downs):
        if ups + downs == 0:
            return 0
        else:
            return _confidence(ups, downs)

��������ʹ���� `����ѷ�÷����� <http://en.wikipedia.org/wiki/Binomial_proportion_confidence_interval#Wilson_score_interval>`_
��ѧ�Ƿ����£�

.. figure:: http://amix.dk/uploads/wilsons_score_interval.png
   :align: center
   :alt: ����ѷ�÷�����

��ʽ�в����������£�

-  p �ǹ۲쵽��֧��Ʊ��ռ�ٷֱ�
-  n ����ͶƱ��
-  z\ :sub:`��/2`\ �� (1-��/2) λ���ı�׼��̬�ֲ�

���ǰ��ϱߵ������ܽ����£�

-  ���������ͶƱ������һ������Ķ�������ͶƱ����ĳ���ͳ�ƣ�������һ��ͶƱѡ��
-  ������������������� 85% �Ŀ��Ŷ�
-  ͶƱ��Խ�࣬85%����Ϣ�÷�Խ�ӽ�����ʵ�÷�
-  ����ѷ�÷������С�����ĳ��Ժͼ��˵ĸ������źܺõ�����  (?)

Randall `������һƪ������ <http://blog.reddit.com/2009/10/reddits-new-comment-sorting-system.html>`_ ��һ���ܺõ����ӽ�����������������θ������������ģ�

    ���һ��������1��������û�в���������֧������100%������������������С��ϵͳ���ǻ�����ŵ��ײ��� �����������10��������1��������ϵͳ���ܻ����㹻����Ϣ�����ŵ�һ������40��������20������������֮ǰ����Ϊ���ǻ���ȷ�ϵ�������40��������ʱ�����յ��Ĳ���������20������õ�һ���ǣ�һ������㷨�����ˣ��㷨��15%��ʧЧ���ʣ�������ܿ��õ���������ݣ���Ϊ�����ŵ���ǰ�档(?)

����ʱ���Ӱ�죺һ�����û��
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

����������е�������������ʱ���޹� (���������� Hacker New ������ͬ)��������ͨ�����ĺ����ݲ����������ġ����磬ͶƱ��Խ�࣬�÷�Ҳ��Խ׼ȷ��

���ӻ�
~~~~~~

����������ͨ��ͼ��һ��������������ζ����������ġ����ǿ��Խ��� Randall ����������:

.. figure:: http://amix.dk/uploads/reddit_confidence_sort.png
   :align: center
   :alt: Reddit ����������

�����㿴���ģ��������򲢲�����һ�����۵�ͶƱ���������ĺ�������ͶƱ�����������С����Թ�ϵ��

����֮���Ӧ��
~~~~~~~~~~~~~~

���� `Evan
Miller <http://www.evanmiller.org/how-not-to-sort-by-average-rating.html>`_
��˵������ѷ�÷����䲻��������������������3�����ӣ�

-  �����ʼ���⣺����������ݲ�������ǳ������ʼ��İٷֱ��ж��٣�
-  ���������б�����������ݲ��������Ǳ���İٷֱ��ж��٣�
-  �������ܻ�Ӧ�б�����������ݲ�����ת�������ѵİٷֱ��ж��٣�

ʹ������㷨��ֻҪ֪�����㣺

-  ͶƱ������
-  Ͷ�޳�Ʊ������

֪��������㷨��������������֮�����뵽�󲿷���վ����ʹ�������ص����������ͻ���úܳԾ�����ʹ�Ǽ�ʮ����Ԫ�Ĵ�˾����������ѷ `Amazon.com <http://amazon.com/>`_ ��������ʽҲ�Ǻܼ򵥣�
ƽ���÷� = ������ / ͶƱ������

����
~~~~

��ϣ����ƪ���¶������ã�������κ�������ǽ��飬���������Ļظ���

Happy hacking as always :)

����Ķ�
~~~~~~~~

-  `Reddit �����������㷨 <http://possiblywrong.wordpress.com/2011/06/05/reddits-comment-ranking-algorithm/>`_,
   ������Reddit����ϵͳ��һ��bug

