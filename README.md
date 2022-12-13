import React, { useState, useEffect } from "react";
import { Input, Button } from "antd";
import data from "./data";
import "styles/org.css";

const TestList = (props) => {
  const { TextArea } = Input;
  const { orgData, onChangeData, device, createInputBox, deleteData } = props;

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

  const onClickDelete = (depth, device) => {
    deleteData(depth, device);
  }

  return (
    <div className="MainDiv">
      <div className="DeviceName">{device}</div>
      <div className="SubBox">
        <div>
          {orgData.map((key, index) => {
            if (key.item.charAt(0, 1) === "L") {
              return (
                <div key={key.item}>
                  <TextArea
                    style={styleObj}
                    defaultValue="총 책임자"
                  ></TextArea>
                  <TextArea
                    onChange={(e) => onChange(e.target.value, index, device)}
                    defaultValue={key.title}
                    style={styleObj}
                  >
                  </TextArea>
                </div>
              );
            } else if (key.item.charAt(0, 1) === "M") {
              return (
                <div key={key.item}>
                  <TextArea
                    style={styleObj}
                    defaultValue="분과 대분류"
                  ></TextArea>
                  <TextArea
                    onChange={(e) => onChange(e.target.value, index, device)}
                    style={styleObj}
                    defaultValue={key.title}
                  ></TextArea>
                </div>
              );
            } else if (key.item.charAt(0, 1) === "B") {
              return (
                <div key={key.item}>
                  <TextArea
                    style={styleObj}
                    defaultValue="Board 위원장"
                  ></TextArea>
                  <TextArea
                    onChange={(e) => onChange(e.target.value, index, device)}
                    style={styleObj}
                    defaultValue={key.title}
                  ></TextArea>
                </div>
              );
            } else if (key.item.charAt(0, 1) === "F") {
              return (
                <div key={key.item}>
                  <TextArea
                    style={styleObj}
                    defaultValue="Facilitator"
                  ></TextArea>
                  <TextArea
                    onChange={(e) => onChange(e.target.value, index, device)}
                    style={styleObj}
                    defaultValue={key.title}
                  ></TextArea>
                </div>
              );
            } else if (key.item.charAt(0, 1) === "C") {
              return (
                <div key={key.item} style={{ position: "relative"}}>
                  <TextArea
                    style={styleObj}
                    defaultValue="분과 분류"
                  ></TextArea>
                  <TextArea
                    onChange={(e) => onChange(e.target.value, index, device)}
                    style={styleObj}
                    defaultValue={key.title}
                  ></TextArea>
                  <div
                    onClick={(e) =>onClickDelete(key.depth, device)}
                    style={{
                      width: 20,
                      height: 20,
                      position: "absolute",
                      zIndex: 1,
                      backgroundColor: "black",
                      top: "0px",
                      right: 0,
                      borderRadius: 20,
                      color: "white",
                      cursor: "pointer",
                      textAlign: "center"
                    }}>x</div>
                </div>
              );
            }
          })}
        </div>
        <div style={{ width: 200}}>
          {orgData.map((key, index) => {
            if (key.depth < 5) {
              return <div key={index} className="NoneBox"></div>;
            } else if (key.depth >= 5 && key.item.charAt(0, 1) === "U") {
              return (
                <TextArea
                  key={key.item}
                  onChange={(e) => onChange(e.target.value, index, device)}
                  style={styleObj}
                  defaultValue={key.title}
                ></TextArea>
              );
            }
          })}
        </div>
      </div>
      <Button onClick={createInputLine} style={{ width: "450px", marginTop: 10}}> 추가 </Button>
    </div>
  );
};

export default TestList;
