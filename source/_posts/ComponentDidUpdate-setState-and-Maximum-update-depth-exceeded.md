---
title: ComponentDidUpdate setState and Maximum update depth exceeded
catalog: true
date: 2019-05-14 11:35:14
subtitle:
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/ComponentDidUpdate-setState-and-Maximum-update-depth-exceeded/header-react-lifecycle.png"
tags:
- React
categories:
- TECH
- FrontEnd
- React
---

# DossierPageIndicatorContainer
一个简单的显示页面页码的pure component，在切换页面（也就是上一回的页码与这次不同时）会显示，过3s消失。
            
Code:          

``` javascript
import classNames from 'classnames';

import PropTypes from 'prop-types';

import React, { Component } from 'react';
import { LiveMessage } from 'react-aria-live';

import { connect } from '../../../utils/PerfUtils';
import { bem } from '../../../utils/CssUtils';

import {
    selectCurrentPageIndex,
    selectDossierPagesCount,
    selectDossierNavBarTitles,
    selectIsShowPageIndicator
} from '../dossierSelectors';

import { formatMessage } from '../../../utils/Intl/IntlUtils';

// component stylesheet
import './styles.scss';

const bemPageIndicator = bem('DossierPageIndicator');

class DossierPageIndicatorContainer extends Component {

    static propTypes = {
        currentPageIndex: PropTypes.number,
        pageCount: PropTypes.number,
        dossierTitles: PropTypes.array,
        left: PropTypes.number.isRequired, //The "left" position of this component
        isShowPageIndicator: PropTypes.bool
    };

    constructor(props) {
        super(props);

        this.state = {
            show: true
        };
    }

    componentDidMount() {
        this.mounted = true;
        this.toggleTimer.call(this);
    }

    componentDidUpdate() {
        this.toggleTimer.call(this);
    }

    componentWillUpdate(nextProps) {
        if (this.props.currentPageIndex !== nextProps.currentPageIndex) {
            this.setState({
                show: true
            });
        }
    }

    componentWillUnmount() {
        this.mounted = false;
    }

    toggleTimer() {
        // Cancel previous pending 'hiding' action if existing
        window.clearTimeout(this.tmr);

        //Hide in 3s
        if (this.state.show) {
            this.tmr = window.setTimeout(
                () => {
                    if (this.mounted) {
                        this.setState({show: false});
                    }
                },
                3000
            );
        }
    }

    render() {
        const { currentPageIndex, pageCount, left, dossierTitles, isShowPageIndicator } = this.props;
        const pageInfo = formatMessage(182, 'Page {currentPage} of {totalPages}', {currentPage: currentPageIndex + 1, totalPages: pageCount});
        // currentPageIndex is default to -1 which means not ready
        // we do not want to render the page indicator when the page is not ready

        const cls = classNames(bemPageIndicator(), {
            'mstrd-show': this.state.show && currentPageIndex >= 0 && pageCount > 0 || isShowPageIndicator
        });

        return (
            <div className={cls} style={{left: left + 'px'}}>
                { pageInfo }
                {!!pageCount && !!dossierTitles.length && <LiveMessage message={`${dossierTitles[currentPageIndex].name} ${pageInfo}`} aria-live="polite"/> }
            </div>
        );
    }
}

function mapStateToProps(state) {
    return {
        currentPageIndex: selectCurrentPageIndex(state),
        pageCount: selectDossierPagesCount(state),
        dossierTitles: selectDossierNavBarTitles(state),
        isShowPageIndicator: selectIsShowPageIndicator(state)
    };
}

export default connect(mapStateToProps, {})(DossierPageIndicatorContainer);
```
# 报错
想增加的效果是： 在第一页（切换上一页）或最后一页（切换下一页）的时候 也显示页码，并且过3s消失。
所以修改代码：

```javascript
    componentWillUpdate(nextProps) {
        if (this.props.currentPageIndex !== nextProps.currentPageIndex || nextProps.currentPageIndex === 0 || nextProps.currentPageIndex === this.props.pageCount - 1) {
            this.setState({
                show: true
            });
        }
    }
```
执行的时候报错：
```
Invariant Violation: Maximum update depth exceeded. dis can happen when a component repeatedly calls setState inside componentWillUpdate or componentDidUpdate. React limits teh number of nested updates to prevent infinite loops.
```

看文档[UNSAFE_componentWillUpdate() react v16.7.0](https://5c54aa429e16c80007af3cd2--reactjs.netlify.com/docs/react-component.html#unsafe_componentwillupdate) 发现不建议再使用componentWillUpdate，而且不建议在componentWillUpdate里setState.

而且这个改法会造成只要是在第一页或最后一页的时候就显示页码，而且不会过3s消失。 而不是切换到第一页或最后一页的时候显示页码并过3s消失。
所以在另一个响应切换页面的事件里dispatch action 来改变state tree里的isShowPageIndicator的值，来表示这个逻辑。
也相应的写好selector和reducer。

# 解决

# Reference Links
[UNSAFE_componentWillUpdate() react v16.7.0](https://5c54aa429e16c80007af3cd2--reactjs.netlify.com/docs/react-component.html#unsafe_componentwillupdate)
