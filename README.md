# DragToDetail
###һ������ʵ�������鿴�������ݵ��Զ���ؼ�������ʵ�������Ӧ������ҳ�棬�����鿴��Ʒ������������<br>�̳���LinearLayout

-----------

##����

-----------
###1.֧�ִ���������ҳ��<br>
###2.֧������������֧�ֺ�������<br>
###3.֧�ֳ�����ListView��ScrollView��HorizontalScrollView��NestedScrollView��RecyclerView��ViewPager��WebView�ȿؼ������ʹ�ã����鿴����Ч��ͼ��<br>
###4.֧��ҳ����������֧�ֹ�������������������һ��ҳ�棬��ϸ˵���뿴ʹ�ý��ܣ�<br>
###5.֧����ת��ָ��ҳ��<br>
###6.��������<br>
<br>

###1.Ч��ͼ1
<br>
![DragToDetail](https://github.com/workdawn/DragToDetail/blob/master/gif/1.gif)

---------

###2.Ч��ͼ2
<br>
![DragToDetail](https://github.com/workdawn/DragToDetail/blob/master/gif/4.gif)

---------

###3.Ч��ͼ3
<br>
![DragToDetail](https://github.com/workdawn/DragToDetail/blob/master/gif/2.gif)

---------

###4.Ч��ͼ4
<br>
![DragToDetail](https://github.com/workdawn/DragToDetail/blob/master/gif/3.gif)

------
<br>

#ʹ��˵��

-------
###1.�������
```
        <declare-styleable name="DragToDetailLayout">
           <!-- ��ק����ϵ�� -->
           <attr name="dragDamp" format="float"/>
           <!-- �ϲ�����ҳ�沼��-->
           <attr name="introLayout" format="reference"/>
           <!-- �²�������ҳ�沼��-->
           <attr name="detailLayout" format="reference"/>
           <!-- �ص���������ʱ�� ��λ������ -->
           <attr name="reboundDuration" format="integer"/>
           <!-- �ص����ʣ�����ȷ���϶����پ��������ʾ��һҳ�� -->
           <attr name="reboundPercent" format="float"/>
       </declare-styleable>
```
####(1).dragDamp����ק����ϵ������ʾ�������ֵ�������С��0.0f - 1.0f��֮�䣬ԽС����ԽС��˵��Խ������ק
####(2).introLayout���Է���һ�������뿴ʹ��DragToDetail�����ַ�����ʹ�ÿؼ�ʱ��ĵ�һҳ�����ļ����ã�<br>����ʾһ��layout�ļ�
####(3).detailLayout���Է���һ�������뿴ʹ��DragToDetail�����ַ�����ʹ�ÿؼ�ʱ��ĵڶ�ҳ�����ļ����ã�<br>����ʾһ��layout�ļ�
####(4).reboundDuration���϶����ֺ󲼾ֵûص�������ת����һҳ�ĳ���ʱ�䣬��λ����
####(5).reboundPercent����ת����һҳ����Ҫ���϶��ٽ����ٷֱȣ�ֵԽ��˵����Ҫ�϶����������ܳ�����ת��һҳ
###2.����ʹ�÷���
####(1).ͨ��introLayout��detailLayout�������������ҳ�棬���ַ�ʽֻ֧������ҳ�棬ͬʱ���ȼ����ߣ���ζ�����ͬʱ������������ҳ�����Ժ��Զ��岼���ӽڵ㣬��ô�ؼ�����Բ����ӽڵ㣩<br>����������������ֻ�ж����ò���Ч��ֻ��������һ���Ļ��ؼ�����Ϊû�и�����
```
        <com.workdawn.dragtodetaillayout.DragToDetailLayout
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:orientation="vertical"
           app:detailLayout="@layout/detail_layout"
           app:introLayout="@layout/intro_layout" />           
```
####(2).ͨ���Զ����Ӳ��ֽڵ㣬��ʹ����ͨ��LinearLayoutһ��
```
        <com.workdawn.dragtodetaillayout.DragToDetailLayout
           android:id="@+id/dd_test"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:orientation="vertical">
   
           <include layout="@layout/intro_layout" />
   
           <include layout="@layout/middle_layout" />
   
           <include layout="@layout/detail_layout" />
   
       </com.workdawn.dragtodetaillayout.DragToDetailLayout>
```
#��Ҫ˵����
##1.��Ϊ���Զ���ؼ��̳���LinearLayout�����Կؼ�����ק����Ҳͬ������LinearLayout��Ҳ����˵�������Ҫһ����ֱ������Ч����ôӦ������DragToDetail��<br>
```
android:orientation="vertical"
````
##ͬʱ�ڲ����Ӳ���ҲҪ����Ϊ��ֱ�������У���ϸʹ�÷�����������demo�鿴��
##2.�����Ҫһ��ˮƽ���������Ч����ôͬ����Ҫ���ò��ֵķ���
```
android:orientation="horizontal"
```
##��ǰˮƽ�������ק֧��HorizontalScrollView��RecyclerView�����ַ���ˮƽ����ViewPager�ȵ���ϣ�������ֱ�������ԵĿؼ��磺ScrollView��ListView��֧�֣�
##����������ViewPager + Fragment�Ļ���Ҫ��ɹ�����ק��ôViewPager��Fragment����������̳��ԣ����������DragFragmentPagerAdapter����DragFragmentStatePagerAdapter<br>����Ҫ��Ϊ���ܻ�ȡ����ǰFragment����Ŀؼ���,ScrollViewAndViewPagerҳ����ʾ�ľ����������
###3.���ֽ������
####������������ĳ��ҳ����¼�����ͨ������EnterDetailLayoutListener��������ʵ��
```
        dragToDetailLayout.setOnEnterDetailLayoutListener(new DragToDetailLayout.EnterDetailLayoutListener() {
            @Override
            public void onEnter(int id) {
                Toast.makeText(DragListenerActivity.this, "����� " + id + "ҳ", Toast.LENGTH_LONG).show();
            }
        });
```
####ͨ���ù��ܿ���ʵ�������������ص����󣬵�����ҳ���ʱ��ų�ʼ����ز��ֿؼ��������������ݵȵȣ����Կ�demo�е�ScrollViewAndViewPagerҳ�棩
###4.ҳ������������ؼ�Ĭ���ṩ�˶Ե�һ��ҳ��Ĺ�������������Ҫ��������ҳ�����ͨ���ؼ��ṩ��getTargetView(int id)������ȡ������Ҫ���������Ŀؼ���������Ӽ���
```
        dragToDetailLayout.setOnDragScrollListener(new DragToDetailLayout.DragScrollListener() {
            @Override
            public void onScrollChanged(View v, float distanceY, float distanceX) {
                tv_scr_distance.setText("��ֱ�����ƶ����� = " + distanceY);
            }
        });
```
###�йػ���������Ҫ˵������ΪView��OnScrollChangeListener����������Android��M�汾��ż�������������������ȫ�汾�Ĺ���������ô��
####(1).��CanListenerScrollView����ScrollView
####(2��.��CanListenerHorizontalScrollView����HorizontalScrollView
####(3��.��CanListenerNestScrollView����NestScrollView
###5.��ת���ض�ҳ�棬��ϸ��鿴SelectItemActivity
```
dragToDetailLayout.setSelectionItem(num);
```