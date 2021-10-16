# Largest-Rectangle-Leetcode-84-

class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        
     stack<pair<int,int>>st;
   vector<int>vec;
   for(int i=0;i<heights.size();i++)
   {
       if(st.size()==0)
       vec.push_back(-1);
       
       else if(st.top().first < heights[i] && st.size()>0)
       vec.push_back(st.top().second);
       
       else if(st.top().first >= heights[i] && st.size()>0)
       {
           while(st.size()>0 && st.top().first >= heights[i])
           {
                   st.pop();
           }
           
           if(st.size()==0)
           vec.push_back(-1);
           else
           vec.push_back(st.top().second);
       }
       st.push({heights[i],i});
   }
    
   while(st.size()>0)
       st.pop();
    
   vector<int>vecr;
   for(int i= heights.size()-1;i>=0;i--)
   {
       if(st.size()==0)
       vecr.push_back(heights.size());
       
       else if(st.top().first < heights[i] && st.size()>0)
       vecr.push_back(st.top().second);
       
       else if(st.top().first >= heights[i] && st.size()>0)
       {
           while(st.size()>0 && st.top().first >= heights[i])
           {
                   st.pop();
           }
           
           if(st.size()==0)
           vecr.push_back(heights.size());
           else
           vecr.push_back(st.top().second);
       }
       st.push({heights[i],i});
   }
    reverse(vecr.begin(),vecr.end());
   
    vector<int>width;
    for(int i=0;i<heights.size();i++)
    {
        width.push_back(vecr[i]- vec[i]-1);
    }
    
    vector<int>area;
    for(int i=0;i<heights.size();i++)
    {
        area.push_back(width[i]*heights[i]);
    }
    return *max_element(area.begin(), area.end());
}
};
