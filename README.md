{


import React, { useState, useEffect } from "react";
import { Input, Button } from "antd";
import "styles/org.css";

const TestList = (props) => {
  const { TextArea } = Input;
  const { orgData, onChangeData, device, createInputBox, deleteData } = props;

  // orgData => data
  // divice => dram, nand ...

  //   const onChangeData = (e, index, device) => {
  //   let copiedItems = [];

  //   if (device === "DRAM") {

  //     copiedItems = [...dramData];

  //     copiedItems[index].title = e;

  //     setDramData(copiedItems);

  //   } else if (device === "NAND") {
  //     copiedItems[1][index].title = e;
  //   } else if (device === "PCM") {
  //     copiedItems[2][index].title = e;
  //   } else if (device === "COMMON") {
  //     copiedItems[3][index].title = e;
  //   }
  // };


  

  const [ data, setData] = useState([]);

  const [firstCheck, setFirstCheck] = useState(false);
  const [secondCheck, setSecondCheck] = useState(false);
  const [thirdCheck, setThirdCheck] = useState(false);
  const [fourthCheck, setFourthCheck] = useState(false);
  const [classCount, setClassCount] = useState(0);

  useEffect( () => {
    if ( orgData !== null ) {
      setData(orgData);

      setFirstCheck(true);
      setSecondCheck(true);
      setThirdCheck(true);


      const classData = orgData.filter(key => key.item.charAt(0,1) !== "U");

      const max = classData.length;

      setClassCount(max);
    } 
  }, [orgData])

  const styleObj = {
    width: 100,
    height: 100,
    display: "inline-flex",
    resize: "none",

    position: "relative",
    zIndex: 0,
  };

  const onChange = (e, index, device) => {
    onChangeData(e, index, device);
  };

  const createInputLine = () => {
    createInputBox(device);
  };

  const onClickDelete = (key) => {
    //deleteData(depth, device);
    if ( key === 3 ) {
      setThirdCheck(false);
      setFourthCheck(false);
    } else if ( key === 2 ) {
      setThirdCheck(false);
      setFourthCheck(false);
    } else if ( key === 1 ) {
      setSecondCheck(false);
      setThirdCheck(false);
      setFourthCheck(false);
    }
  }

  const classBoxCreate = () => {
    let boxArr = [];

    for( let index =0; index<classCount; index++) {
      if( orgData[index].item.charAt(0,1) === "L") {
        boxArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}>총책임자</div>);
      } else if( orgData[index].item.charAt(0,1) === "M") {
        boxArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}>분과 대분류</div>);
      } else if( orgData[index].item.charAt(0,1) === "B") {
        boxArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}>Board 위원장</div>);
      } else if( orgData[index].item.charAt(0,1) === "F") {
        boxArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}>Facilitator</div>);
      } else {
        boxArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}>분과 분류</div>);
      }
    }

    return boxArr;
  }

  const createBox = (key) => {
    if ( key === 2 ) {
      setThirdCheck(true);
    } else if ( key === 1 ) {
      setSecondCheck(true);
    }
  }

  const dataBox = (key) => {
    let dataArr = [];

    if ( key === "class") {
      let classData = data.filter(key => key.item.charAt(0,1) !== "U");


      for( let index =0; index<classCount; index++) {
        if( orgData[index].item.charAt(0,1) === "L") {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{classData[index].title}
          {secondCheck === true ? <Button onClick={(e) => onClickDelete(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button onClick={(e) => createBox(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        } else if( orgData[index].item.charAt(0,1) === "M") {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{classData[index].title}
          {secondCheck === true ? <Button onClick={(e) => onClickDelete(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button onClick={(e) => createBox(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        } else if( orgData[index].item.charAt(0,1) === "B") {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{classData[index].title}
          {secondCheck === true ? <Button onClick={(e) => onClickDelete(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button onClick={(e) => createBox(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        } else if( orgData[index].item.charAt(0,1) === "F") {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{classData[index].title}
          {secondCheck === true ? <Button onClick={(e) => onClickDelete(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button onClick={(e) => createBox(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        } 
        else {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{classData[index].title}
          {secondCheck === true ? <Button onClick={(e) => onClickDelete(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button onClick={(e) => createBox(1)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        }
      }
    } else if ( key === "firstUser") {
      let userData = data.filter(key => (
        key.item.charAt(0,1) !== "U" &&
        key.item.charAt(0,1) !== "C" ||
        key.item.charAt(0,1) === "U" &&
        parseInt(key.item.charAt(key.item.length-1))%2 !== 0
      ));

      for( let index =0; index<classCount; index++) {
        if( userData[index].item.charAt(0,1) !== "U") {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px"}}></div>);
        } else {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{userData[index].title}
          {thirdCheck === true ? <Button onClick={(e) => onClickDelete(2)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button onClick={(e) => createBox(2)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        }
      }
    } else if ( key === "secondUser") {
      let userData = data.filter(key => (
        key.item.charAt(0,1) !== "U" &&
        key.item.charAt(0,1) !== "C" ||
        key.item.charAt(0,1) === "U" &&
        parseInt(key.item.charAt(key.item.length-1))%2 !== 1
      ));

      for( let index =0; index<classCount; index++) {
        if( userData[index].item.charAt(0,1) !== "U" ) {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px"}}></div>);
        } else {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center", position: "relative"}}>{userData[index].title}
            { fourthCheck === true ? 
            <Button onClick={(e) => onClickDelete(3)} style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>X</Button> :
            <Button style={{ position: "absolute", borderRadius: 200, top: 0, right: 0}}>+</Button>
          }
          </div>);
        }
      }
    }

    return dataArr;
  }

  const emptyBox = (key) => {

    let dataArr = [];

    if ( key === "class") {
      for( let index =0; index<classCount; index++) {
        if( index === 0) {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}> + </div>);
        } else if( index === 1) {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}> + </div>);
        } else if( index === 2) {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}> + </div>);
        } else if( index === 3) {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}> + </div>);
        } else {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}> + </div>);
        }
      }
    } else if ( key === "firstUser") {

      let userData = data.filter(key => (
        key.item.charAt(0,1) !== "U" &&
        key.item.charAt(0,1) !== "C" ||
        key.item.charAt(0,1) === "U" &&
        parseInt(key.item.charAt(key.item.length-1))%2 !== 0
      ));

      for( let index =0; index<classCount; index++) {
        if( userData[index].item.charAt(0,1) !== "U") {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px",}}></div>);
        } else {
          dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black", textAlign: "center"}}> + </div>);
        }
      }
    } else if ( key === "secondUser") {
      if ( secondCheck === true ) {
      let userData = data.filter(key => (
        key.item.charAt(0,1) !== "U" &&
        key.item.charAt(0,1) !== "C" ||
        key.item.charAt(0,1) === "U" &&
        parseInt(key.item.charAt(key.item.length-1))%2 !== 1
      ));
      
        for( let index =0; index<classCount; index++) {
          if( userData[index].item.charAt(0,1) !== "U" ) {
            dataArr.push(<div key={index} style={{ width: "100%", height: "50px", textAlign: "center"}}></div>);
          } else {
            dataArr.push(<div key={index} style={{ width: "100%", height: "50px", border: "1px solid black",textAlign: "center"}}> + </div>);
          }
        }
      }
    }
    return dataArr;
  }

  return (
    <div className="MainDiv">
      <div className="DeviceName">{device}</div>
      <div style={{ display: "inline-flex"}}>
        <div style={{ width: 200, height: 1000, display: "inline-block"}}>
          {classBoxCreate()}
        </div>
        <div style={{ width: 200, height: 1000, display: "inline-block"}}>
          { firstCheck === true ? dataBox("class") : emptyBox("class")}
        </div>
        <div style={{ width: 200, height: 1000, display: "inline-block"}}>
          { secondCheck === true ? dataBox("firstUser") : emptyBox("firstUser")}
        </div>
        <div style={{ width: 200, height: 1000, display: "inline-block"}}>
          { thirdCheck === true ? dataBox("secondUser") : emptyBox("secondUser")}
        </div>
        </div>
    </div>
  );
};

export default TestList;



}
