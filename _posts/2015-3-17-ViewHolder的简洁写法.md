---
layout:	post
title:	"ViewHolder模式的一种简洁写法"
date:	2015-03-18 17:30:00
categories:	android
---

我们经常用的ViewHolder的写法如下：

	@Override
	public View getView(int position, View convertView, ViewGroup parent) {

	    ViewHolder viewHolder = null;
		if(convertView == null){
			convertView = mInflate.inflate(R.layout.xxx, parent, false);
			viewHolder = new ViewHolder();
			//...一连串的viewHolder.xxx = findViewById(R.id.xx);
			convertView.setTag(viewHolder);
		}else{
			viewHolder = (ViewHolder)convertView.getTag();
			//...viewHolder.xxx取出
		}

	}

	private static class ViewHolder{
		
		//需要使用的View的定义
	}

<!-- more -->

但是往往我们在一个项目中要用到多个Adapter，每一个Adapter都得重复的这样写确实很不爽，那么有没有一种方法在一个类里完成，然后在每个Adapter里直接调用呢？

下面来看国外网站上大牛的简洁设计：

	public class ViewHolder{
		
		public static <T extends View> T get(View view, int id){

			SparceArray<View> viewHolder = (SparceArray<View>)view.getTag();
			if(viewHolder == null){
				viewHolder = new SparceArray<View>();
				view.setTag(viewHolder);
			}

			View childView = ViewHolder.get(id);
			if(childView == null){
				childView = findViewById(id);
				viewHolder.put(id,childView);
			}
			return (T)childView;
		}

	}

下面在Adapter里重写getView方法：

	@Override
	public View getView(int position, View convertView, ViewGroup parent){
		
		if(convertView == null){
			convertView = mInflate.inflate(R.layout.xxx, parent, false);
		}
		
		//各种需要用到的View初始化
		ImageView image = (ImageView)ViewHolder.get(convertView, R.id.xxx);
		TextView text = (TextView)ViewHolder.get(convertView, R.id.xxx);

		return convertView;
	}

好了，通过上面的写法，我们就只需要完成了ViewHolder类，在Adapter中的getView方法中调用get方法就好了，一劳永逸！
